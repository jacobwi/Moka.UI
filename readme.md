name: Publish Package
on:
  push:
    tags:
      - 'v*'

permissions:
  contents: write
  packages: write

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - name: Setup .NET
        uses: actions/setup-dotnet@v4
        with:
          dotnet-version: 7.0.x  # Changed to .NET 7 as per your requirements

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '18'

      - name: Install Dependencies
        run: yarn install

      - name: Build Assets
        run: yarn build

      - name: Get Version
        id: version
        shell: bash
        run: |
          VERSION=${GITHUB_REF#refs/tags/v}
          echo "version=$VERSION" >> $GITHUB_OUTPUT
          echo "version-without-v=$VERSION" >> $GITHUB_OUTPUT

      - name: Pack
        run: dotnet pack --configuration Release /p:Version=${{ steps.version.outputs.version-without-v }} -p:PackageId=Midmoka.UI --output .

      # Add GitHub Packages source
      - name: Add GitHub Source
        run: |
          dotnet nuget add source --username jacobwi --password ${{ secrets.GITHUB_TOKEN }} --store-password-in-clear-text --name github "https://nuget.pkg.github.com/jacobwi/index.json"

      # Push to GitHub Packages
      - name: Push to GitHub Packages
        run: |
          dotnet nuget push *.nupkg --source "github" --api-key ${{ secrets.GITHUB_TOKEN }} --skip-duplicate

      # Push to NuGet.org
      - name: Push to NuGet
        run: |
          dotnet nuget push *.nupkg --source https://api.nuget.org/v3/index.json --api-key ${{ secrets.NUGET_API_KEY }} --skip-duplicate

      - name: Create Release
        uses: ncipollo/release-action@v1
        with:
          artifacts: "*.nupkg"
          name: Release ${{ steps.version.outputs.version }}
          body: |
            Release of version ${{ steps.version.outputs.version }}
           
            ### What's Changed
            - Blazor components wrapping Bulma CSS framework
            - Responsive design support
            - Customizable theming
            - Interactive components
            - Font Awesome integration
           
            ### Getting Started
            ```html
            <!-- Add to your _Host.cshtml or index.html -->
            <link href="_content/Midmoka.UI/css/midmoka.css" rel="stylesheet" />
            ```

            ```csharp
            // Add to your Program.cs
            builder.Services.AddMidmokaUI();
            ```
          draft: true
          allowUpdates: true