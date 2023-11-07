# 🚀 Midmoka.UI - Bulma Blazor Components

[![NuGet](https://img.shields.io/nuget/v/Moka.Editor.Md.svg)](https://www.nuget.org/packages/Moka.Editor.Md/) [![NuGet](https://img.shields.io/nuget/dt/Moka.Editor.Md.svg)](https://www.nuget.org/packages/Moka.Editor.Md/)

## Introduction 📖

Midmoka.UI is a Blazor class library that wraps [Bulma](https://bulma.io/) 🎨, a modern CSS framework, into reusable Blazor components. With Midmoka.UI, you can build responsive 📱 web applications with beautiful components, leveraging both Blazor's powerful C# capabilities 🔥 and Bulma's sleek styling ✨.

## Features ✨

- 🎨 **Theming**: Customize components with Bulma variables and your own themes.
- 🧱 **Reusable Components**: Use out-of-the-box components for faster development.
- 📱 **Responsive**: Build websites that look great on all devices.
- 🔧 **Customizable**: Adjust components with a wide range of parameters and options.
- 🎉 **Interactive Demos**: See components in action with live examples.

## Getting Started

### Prerequisites

Ensure you have the following installed:

- .NET 7.0+
- Node.js
- Yarn/Node package manager

### Installation

1. Install the necessary Node.js packages:

```bash
yarn
```

2. Run the Gulp tasks to bundle and prepare your assets:

```bash
yarn build
```

3. Build the library:

```bash
dotnet build
```

### Usage

After installing the package and running Gulp tasks, simply reference the bundled files in your header tag in index HTML
file.
For CSS:

```html
<link href="_content/Moka.UI/css/midmoka.css" rel="stylesheet" />
```


### 🍷 Gulp Tasks

I use Gulp to automate the bundling and optimization of assets. Here's what each task does:

- styles: Concatenates and minifies CSS files and includes Font Awesome styles.
- default: Runs all the above tasks in sequence.
  You can run a specific task with the following command:

```
yarn gulp <task-name>
```

For example, to only run the styles task:

```bash
yarn gulp styles
```

### 🫂 Contributing

Contributions are welcome as this is an open-source project in such an amazing place to learn, inspire, and create. Any
contributions you make are greatly appreciated.

#### 🪜 Steps:

- Fork the Project
- Create your Feature Branch (git checkout -b feature/AmazingFeature)
- Commit your Changes (git commit -m 'Add some AmazingFeature')
- Push to the Branch (git push origin feature/AmazingFeature)
- Open a Pull Request

### License

Distributed under the MIT License. See LICENSE for more information.

🫡 Jacob William - me@jacobwi.net

### WIP

- [x] Add Bulma
- [ ] Upload to NuGet
- [ ] Add more tests
- [ ] Add more documentation
- [ ] Add more examples
- [ ] Add more features