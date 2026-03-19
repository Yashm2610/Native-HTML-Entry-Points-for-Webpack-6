Native HTML Entry Points for Webpack 6
Overview

Webpack is one of the most widely used module bundlers for modern web applications. Traditionally, webpack requires JavaScript files as entry points, meaning developers must configure additional plugins to integrate HTML files into the build process.

This project introduces native HTML entry point support in Webpack 6, allowing developers to directly specify an HTML file as the entry in the webpack configuration. Webpack will automatically parse the HTML file, detect referenced assets such as JavaScript, CSS, and images, and include them in the dependency graph for bundling and optimization.

The goal of this project is to simplify configuration, improve developer experience, and align webpack's build model with how browsers load web pages.

Motivation

Currently, developers must rely on plugins like HtmlWebpackPlugin or other third-party tools to integrate HTML into the webpack build pipeline. This creates several challenges:

Extra configuration for basic setups

Additional dependencies to maintain

More complexity for multi-page applications

A mismatch between browser behavior and webpack's entry model

By enabling HTML as a first-class entry point, webpack will provide a simpler and more intuitive development workflow.

Key Features

Native HTML Entry Support

Use HTML files directly as webpack entry points.

Automatic Asset Detection

Parses HTML files and detects:

<script src>

<link rel="stylesheet">

<img src>

<source srcset>

Dependency Graph Integration

All extracted assets become part of webpack's module graph.

Optimized Asset Bundling

Supports hashing, code splitting, and caching automatically.

Output HTML Generation

Rewrites asset URLs to match generated bundles.

Hot Module Replacement (HMR)

HTML changes trigger page reloads while JS/CSS maintain hot updates.

Example Usage
Basic Configuration
// webpack.config.js
module.exports = {
  entry: "./src/index.html"
};
Multi-Page Application
// webpack.config.js
module.exports = {
  entry: {
    home: "./src/pages/home.html",
    about: "./src/pages/about.html"
  }
};

Webpack will automatically process the HTML files and bundle all referenced assets.

Architecture

The implementation introduces a new internal plugin called HtmlEntryPlugin.

Workflow

Entry Detection

Webpack detects .html files in the entry configuration.

HTML Parsing

Extracts asset references from HTML.

Dependency Creation

Each referenced asset becomes a webpack dependency.

Module Graph Integration

Assets are included in webpack's existing dependency graph.

Bundle Generation

Webpack bundles all assets and optimizes them.

HTML Output

Generated bundles are injected into the final HTML output.

Project Structure (Conceptual)
webpack/
 ├── lib/
 │   ├── EntryPlugin.js
 │   ├── HtmlEntryPlugin.js
 │   ├── dependencies/
 │   │   └── HtmlDependency.js
 │   ├── generators/
 │   │   └── HtmlGenerator.js
 │
 ├── test/
 │   └── html-entry-tests
 │
 └── examples/
     └── html-entry-example
Development Setup
Clone the repository
git clone https://github.com/webpack/webpack
cd webpack
Install dependencies
npm install
Run tests
npm test
Deliverables

HTML entry detection in webpack configuration

HTML parser for extracting asset dependencies

Integration with webpack module graph

Asset bundling and optimized HTML output

Hot Module Replacement support

Documentation and usage examples

Timeline (GSoC 2026)
Phase	Duration	Goal
Community Bonding	May	Codebase study and design finalization
Phase 1	Weeks 1–4	HTML entry detection and parser prototype
Phase 2	Weeks 5–8	Dependency graph integration and bundling
Phase 3	Weeks 9–12	HMR support, testing, documentation
Final	Final Week	Code polishing and submission
Future Enhancements

Template engine support (EJS, Handlebars)

HTML minification options

Plugin hooks for HTML transformations

Advanced asset optimization features

References

https://webpack.js.org

https://github.com/webpack/webpack/issues/536

https://github.com/webpack/webpack/issues/7589

https://webpack.js.org/contribute/
