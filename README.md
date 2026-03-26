# React PDF REPL

A modern, interactive web-based REPL (Read-Eval-Print Loop) for creating and debugging PDF files using React. This project allows developers to write React components that render to PDF format, with live preview, debugging tools, and a comprehensive development environment.

**Live Demo:** https://react-pdf-repl.vercel.app/

## Overview

React PDF REPL is a full-featured development environment for building PDF documents with React and [@react-pdf/renderer](https://react-pdf.org/). It provides:

- **Live Code Editor** - Monaco Editor for writing React components
- **Real-time PDF Preview** - Instantly see your changes rendered as PDFs
- **PDF Debugging Tools** - Inspect PDF structure, elements, and box sizing
- **Code Sharing** - Compress and share code via URL parameters
- **Module Support** - Write modular code with ES6 imports
- **Error Handling** - Clear error messages with recovery options
- **Responsive UI** - Resizable panels for optimal workflow

## Features

### Core Features
- 🎯 **Instant Feedback** - See PDF changes in real-time as you edit code
- 🔍 **Interactive Debugger** - Inspect PDF element tree with hover previews
- 📐 **Box Model Debugging** - Visualize element borders, margins, and padding
- 🎨 **Syntax Highlighting** - Full Monaco Editor support with IntelliSense
- 📦 **Module System** - Use ES6 modules with automatic code transformation
- 🔗 **URL Code Sharing** - Share code via compressed URL parameters
- 🐳 **Sandpack Integration** - Alternative sandbox environment for examples

### Advanced Capabilities
- **Secure Code Execution** - Uses SES (Secure EcmaScript) for sandboxed evaluation
- **Web Worker Support** - Non-blocking code execution with worker threads
- **PDF.js Integration** - Full PDF viewer with page navigation
- **Layout Tracking** - Capture and inspect PDF layout data
- **Canvas Pooling** - Optimized rendering with canvas reuse
- **Responsive Panels** - Resizable interface with react-resizable-panels

## Project Structure

```
react-pdf-repl/
├── app/                          # Next.js 13 App Router
│   ├── page.js                  # Main REPL page
│   ├── repl.js                  # REPL component (client-side)
│   ├── layout.js                # Root layout
│   ├── globals.css              # Global styles
│   └── sandpack/                # Sandpack sandbox environment
│       ├── page.js              # Sandpack page
│       └── example/             # Example code files
│
├── components/                   # React components
│   ├── repl-layout.js           # Main REPL layout structure
│   ├── viewer.js                # PDF viewer component
│   ├── debug-tree.js            # PDF element tree debugger
│   ├── elements-tree.js         # Interactive element tree
│   ├── box-sizing.js            # Box model indicator
│   └── *.module.css             # Component styles
│
├── state/                        # Jotai state management
│   ├── debugger.js              # Debugger state (layout, selection, hover)
│   └── page.js                  # PDF page navigation state
│
├── hooks/                        # Custom React hooks
│   └── index.js                 # createSingleton, useEventCallback, etc.
│
├── worker/                       # Web Worker files
│   ├── index.js                 # Worker wrapper and lifecycle
│   ├── executer.js              # Code execution engine
│   ├── process-jsx.js           # JSX preprocessing (Acorn + Astring)
│   ├── to-module.js             # ES6 module compilation
│   └── better-static-module-record.mjs  # Compartment integration
│
├── code/                        # Default code examples
│   ├── default-example.js       # Demo code snippets
│   └── lz.js                    # LZ-string compression utilities
│
├── pages/
│   └── api/
│       └── og.js                # Open Graph image generation
│
├── patches/                     # Package patches
│   └── pdfjs-dist+3.3.122.patch
│
├── public/                      # Static assets
│
├── package.json                 # Dependencies and scripts
├── next.config.js               # Next.js configuration
└── README.md                    # This file
```

## Technology Stack

### Core Framework
- **Next.js 13** - React framework with App Router
- **React 18.2** - UI library
- **React Server Components** - Server-side rendering

### PDF & Document Processing
- **@react-pdf/renderer** - React to PDF rendering
- **pdfjs-dist** - PDF viewing and manipulation
- **react-pdf-tailwind** - Tailwind CSS utilities for PDF
- **Canvas API** - Low-level PDF rendering
- **@napi-rs/canvas** - Node.js canvas support

### Code Editing & Execution
- **@monaco-editor/react** - Visual Studio Code editor
- **Acorn & Acorn-JSX** - JavaScript/JSX parsing
- **Astring** - AST to code generation
- **estree-util-build-jsx** - JSX transformation
- **SES (Secure EcmaScript)** - Sandboxed code evaluation
- **@endo/static-module-record** - Module record support

### State Management & UI
- **Jotai** - Primitive and flexible state management
- **react-resizable-panels** - Resizable panel layout
- **@react-hook/resize-observer** - Size observation
- **react-suspense-fetch** - Data fetching with Suspense

### Utilities
- **lz-string** - Compression for URL code sharing
- **@vercel/analytics** - Analytics integration
- **next-axiom** - Observability and logging
- **patch-package** - Patch management

## Getting Started

### Prerequisites
- Node.js 16+ or compatible environment
- npm or yarn package manager

### Installation

```bash
# Clone the repository
git clone https://github.com/jeetiss/react-pdf-repl.git
cd react-pdf-repl

# Install dependencies
npm install

# Apply patches
npm run postinstall
```

### Development

```bash
# Start development server
npm run dev

# Open in browser
# http://localhost:3000
```

The application will start with hot-reload enabled. Changes to code and components will instantly reflect in the browser.

### Production Build

```bash
# Build for production
npm run build

# Start production server
npm start

# Run linting
npm run lint
```

## Usage

### Writing PDF Documents

The REPL expects a **default export** of a React component that renders a PDF document using `@react-pdf/renderer`:

```jsx
import { Document, Page, Text } from '@react-pdf/renderer';

export default () => (
  <Document>
    <Page>
      <Text>Hello, World!</Text>
    </Page>
  </Document>
);
```

### Creating Styled Documents

Use `StyleSheet` for performance-optimized styles:

```jsx
import { StyleSheet, Document, Page, View, Text } from '@react-pdf/renderer';

const styles = StyleSheet.create({
  page: {
    padding: 40,
  },
  text: {
    fontSize: 12,
    color: '#333',
  },
});

export default () => (
  <Document>
    <Page style={styles.page}>
      <Text style={styles.text}>Styled PDF</Text>
    </Page>
  </Document>
);
```

### Using Tailwind CSS

For rapid styling with Tailwind utilities:

```jsx
import { Document, Page, Text } from '@react-pdf/renderer';
import { tw } from 'react-pdf-tailwind';

export default () => (
  <Document>
    <Page style={tw('p-8')}>
      <Text style={tw('text-base')}>Tailwind Styled</Text>
    </Page>
  </Document>
);
```

### Modular Code

Write modular code with ES6 imports:

```jsx
// components/Header.jsx
import { Text, View } from '@react-pdf/renderer';

export const Header = () => (
  <View>
    <Text>Document Header</Text>
  </View>
);

// Main component
import { Document, Page } from '@react-pdf/renderer';
import { Header } from './components/Header';

export default () => (
  <Document>
    <Page>
      <Header />
    </Page>
  </Document>
);
```

### Debugging

The REPL includes powerful debugging tools:

1. **Element Tree** - Click to inspect PDF elements
2. **Box Sizing** - Visualize spacing and dimensions
3. **Page Navigation** - Navigate multi-page documents
4. **Error Viewer** - Clear error messages with recovery options
5. **Layout Inspector** - Examine computed layout data

### URL Code Sharing

Share code via compressed URL parameters:

- Use the app interface to generate shareable links
- Code is compressed with LZ-string compression
- Query parameters: `cp_code` (custom code) or `gz_code` (compressed code)

Example:
```
https://react-pdf-repl.vercel.app/?gz_code=eJxlkcFq...
```

## Architecture

### Code Execution Pipeline

```
User Code (JSX)
    ↓
Parser (Acorn JSX)
    ↓
JSX Transform (estree-util-build-jsx)
    ↓
AST Generation (Astring)
    ↓
Module Compilation (StaticModuleRecord)
    ↓
Sandboxed Evaluation (SES Compartment)
    ↓
React Component Rendering
    ↓
@react-pdf/renderer
    ↓
PDF Blob
```

### Component Hierarchy

```
App (page.js)
├── Repl (repl.js)
│   ├── Editor (Monaco)
│   ├── ErrorBoundary
│   ├── PanelGroup (ResizablePanel)
│   │   ├── EditorPanel
│   │   ├── PreviewPanel
│   │   │   ├── Viewer (PDF viewer)
│   │   │   ├── DebugTree (Element tree)
│   │   │   └── BoxSizing (Box model)
│   │   └── DebugPanel
│   └── Controls (navigation, buttons)
```

### State Management (Jotai)

- **layoutAtom** - PDF element tree state
- **selectedAtom** - Currently selected element
- **hoverAtom** - Hovered element path
- **pageAtom** - Current page number
- **urlAtom** - Generated PDF URL

### Web Worker

The code execution runs in a Web Worker to prevent blocking the main thread:

1. User code is sent to worker via `postMessage`
2. Worker executes code in SES Compartment
3. PDF is generated and converted to Blob
4. URL and layout data returned to main thread

## Key Concepts

### SES (Secure EcmaScript)

Code runs in isolated SES Compartments with restricted globals:
- Only approved APIs are available
- No access to DOM or window object
- Safe cross-component code evaluation

### Layout Capturing

The REPL captures PDF layout information by wrapping the Document component with a LayoutProvider that intercepts render callbacks.

### Module Records

Code is compiled into ES6 module records using `StaticModuleRecord`, enabling:
- Import/export support
- Scoped variable isolation
- Virtual module filesystem

### Canvas Pooling

To optimize rendering performance, PDF canvases are reused:
- Rendered canvases are pooled after use
- New renders reuse pooled canvases when possible
- Reduces memory allocation overhead

## Development Tips

### Adding New Dependencies

```bash
npm install <package-name>
npm run postinstall  # Apply patches
```

### Modifying Worker

Changes to `/worker` files require page reload (not hot-reload):
- Web Workers cannot be HMR'd directly
- Restart dev server for changes to take effect

### Debugging Worker Execution

Use `console.log` inside worker code - messages appear in browser console.

### Custom PDF Styling

All `@react-pdf/renderer` styling is supported:
- Flexbox layouts
- Colors and backgrounds
- Transform and opacity
- Fonts and typography
- Page breaks

## Configuration

### Next.js Configuration

Key settings in `next.config.js`:
- **App Router** - Enabled experiments.appDir
- **Output Tracing** - Disabled for worker support
- **Webpack Rules** - PDF worker asset handling
- **Raw Asset Loading** - For Sandpack examples

### Environment Variables

Optional environment configuration:
- No required environment variables for local development
- Vercel Analytics integrated via `next-axiom`

## Deployment

### Vercel

Optimized for Vercel deployment:

```bash
npm run build
```

The application includes:
- Open Graph image generation
- Request logging via next-axiom
- Automatic redirects for legacy URLs

### Docker / Self-Hosted

```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY . .
RUN npm install
RUN npm run build
EXPOSE 3000
CMD ["npm", "start"]
```

## Troubleshooting

### Error: "The default export is not a React PDF Component"

Ensure your code exports a valid React component that renders to PDF:
```jsx
export default () => <Document>...</Document>;
```

### Code Won't Execute / Worker Timeout

- Check browser console for syntax errors
- Validate JSX syntax
- Ensure no infinite loops
- Worker has default 30s timeout

### PDF Not Showing

- Verify component renders a `<Document>` with `<Page>` children
- Check for console errors
- Ensure valid @react-pdf/renderer usage

### Module Not Found

- Check module names match import statements
- Relative imports require `./` or `../` prefix
- Only top-level modules can be imported

## Performance Optimization

### Best Practices

1. **Use StyleSheet** - Improves rendering performance
2. **Memoize Components** - Cache expensive computations
3. **Lazy Load** - Dynamically import large modules
4. **Optimize Images** - Use appropriately sized assets
5. **Avoid Dynamic Styles** - Pre-compute styles outside render

### Limits

- Max uncompressed code: Limited by browser memory
- Max PDF size: Depends on system resources
- Worker timeout: ~30 seconds default
- Page count: Tested up to 1000+ pages

## Contributing

Contributions are welcome! Areas for improvement:

- Additional debugging features
- Performance optimizations
- More example templates
- Enhanced error messages
- Accessibility improvements

## License

ISC License - Copyright 2023 Dmitry Ivakhnenko

See [LICENSE](LICENSE) file for details.

## Resources

### Official Documentation
- [@react-pdf/renderer](https://react-pdf.org/)
- [Next.js 13](https://nextjs.org/docs)
- [React 18](https://react.dev/)
- [Jotai](https://jotai.org/)
- [Monaco Editor](https://microsoft.github.io/monaco-editor/)

### Related Tools
- [PDF.js](https://mozilla.github.io/pdf.js/)
- [SES](https://github.com/endojs/endo)
- [Sandpack](https://sandpack.codesandbox.io/)

## Support

- **GitHub Issues** - https://github.com/jeetiss/react-pdf-repl/issues
- **Live Demo** - https://react-pdf-repl.vercel.app/
- **Author** - Dmitry Ivakhnenko

## Changelog

### v0.1.0 (Current)
- Initial release
- Core REPL functionality
- PDF debugging tools
- URL code sharing
- Sandpack integration
- Module support

---

**Made with ❤️ for PDF enthusiasts and React developers**
