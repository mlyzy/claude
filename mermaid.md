# Mermaid.js Installation and Testing

This document summarizes the process of downloading, installing, and testing the [Mermaid.js](https://github.com/mermaid-js/mermaid) project, a JavaScript-based diagramming and charting tool that renders Markdown-inspired text definitions to create and modify diagrams dynamically.

## Project Overview

Mermaid.js allows users to create diagrams and visualizations using text and code. The library is designed to be simple to use and renders diagrams based on Markdown-inspired syntax. It supports various diagram types including:

- Flowcharts
- Sequence diagrams
- Class diagrams
- Entity Relationship diagrams
- State diagrams
- Gantt charts
- Pie charts
- Git graphs
- And more

The project is structured as a monorepo using pnpm as its package manager.

## Environment Setup

### Prerequisites
- Git
- Node.js and npm (we used Node.js v18.20.8)
- pnpm (Node.js package manager)

### Installation Steps

1. **Install Node Version Manager (nvm)**
   ```bash
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
   ```
   This allows for easy management of Node.js versions.

2. **Install Node.js using nvm**
   ```bash
   export NVM_DIR="$HOME/.nvm"
   [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
   nvm install 18
   ```
   This installed Node.js v18.20.8 and npm v10.8.2.

3. **Clone the repository**
   ```bash
   git clone https://github.com/mermaid-js/mermaid.git
   ```
   This created a local copy of the mermaid repository.

4. **Install pnpm globally**
   ```bash
   npm install -g pnpm
   ```
   pnpm is required as the project uses it for dependency management.

5. **Install project dependencies**
   ```bash
   cd mermaid
   pnpm install
   ```
   This installed all required dependencies for the project and built the necessary components.

## Building the Project

The installation process automatically triggered the build process due to the `prepare` script in package.json. The build process completed the following steps:

1. **Built the esbuild packages**
   ```bash
   pnpm build:esbuild
   ```
   This compiled the source code using esbuild.

2. **Generated TypeScript types**
   ```bash
   pnpm build:types
   ```
   This generated TypeScript type definitions.

The build process created the following output artifacts:
- Core library files (`mermaid.core.mjs`)
- ESM modules (`mermaid.esm.mjs`)
- Minified bundles (`mermaid.min.js`)
- Sourcemaps for debugging
- TypeScript type definitions

## Running the Development Server

To start the development server, we ran:
```bash
pnpm dev
```

This started a local development server at http://localhost:9000/, which served a page with examples and testing capabilities.

## Testing the Project

We tested the project through the development server:

1. **Development Page**: Accessed http://localhost:9000/dev/example.html to view and test custom mermaid diagram code.

2. **Example Diagrams**: Explored the various diagram types available through the menu links at http://localhost:9000/. The examples showcase different diagram types and syntax.

3. **Flow Chart Example**: Tested the flowchart implementation, which demonstrated the capability to create complex flow diagrams with various node shapes, connectors, and styles.

## Project Structure

The project is organized as a monorepo with several packages:

- `packages/mermaid` - The core mermaid library
- `packages/parser` - Parser components
- `packages/mermaid-example-diagram` - Example diagram implementation
- `packages/mermaid-zenuml` - ZenUML integration
- `packages/mermaid-layout-elk` - ELK layout engine integration
- `packages/tiny` - Smaller components

## Conclusion

Mermaid.js is a robust diagramming library that provides an easy way to create and display diagrams using text-based descriptions. The project is well-structured, actively maintained, and offers comprehensive examples and documentation. It successfully renders various diagram types and provides a development environment for testing and extending the library.

The version we tested (v11.6.0) shows good performance and a wide range of diagram types. The development server provides a useful environment for testing custom diagram code and exploring the library's capabilities.
