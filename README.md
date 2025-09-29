# Hello WebAssembly with Rust

A simple example project demonstrating how to build and use WebAssembly modules with Rust and wasm-bindgen.

## Prerequisites

Before running this project, make sure you have the following installed:

- [Rust](https://rustup.rs/) (latest stable version)
- [wasm-pack](https://rustwasm.github.io/wasm-pack/installer/)

### Install wasm-pack

```bash
curl https://rustwasm.github.io/wasm-pack/installer/init.sh -sSf | sh
```

## Project Structure

```
hello-wasm/
├── Cargo.toml          # Rust project configuration
├── src/
│   └── lib.rs          # Rust source code with WebAssembly bindings
├── pkg/                # Generated WebAssembly package
├── index.html          # HTML file to test the WebAssembly module
└── README.md
```

## Building the Project

1. **Clone the repository** (if you haven't already):
   ```bash
   git clone <repository-url>
   cd hello-wasm
   ```

2. **Build the WebAssembly module**:
   ```bash
   wasm-pack build --target web
   ```

   This command will:
   - Compile the Rust code to WebAssembly
   - Generate JavaScript bindings
   - Create TypeScript definitions
   - Output everything to the `pkg/` directory

## Running the Project

Since browsers require CORS for ES modules, you need to serve the files through a local server:

### Option 1: Using Python (if installed)
```bash
# Python 3
python -m http.server 8000

# Python 2
python -m SimpleHTTPServer 8000
```

### Option 2: Using Node.js
```bash
# Install a simple HTTP server
npm install -g http-server

# Serve the files
http-server
```

### Option 3: Using PHP (if installed)
```bash
php -S localhost:8000
```

### Option 4: Using VS Code Live Server
If you're using VS Code, install the "Live Server" extension and right-click on `index.html` to select "Open with Live Server".

## Testing

1. After starting the local server, open your browser and navigate to:
   ```
   http://localhost:8000
   ```

2. Open the browser's developer console (F12)

3. You should see the message: `Hello from Rust, Rustacean!`

## How It Works

1. **Rust Code** (`src/lib.rs`): Contains a simple `greet` function that takes a name and returns a greeting string.

2. **WebAssembly Compilation**: The `wasm-pack` tool compiles the Rust code to WebAssembly and generates JavaScript bindings.

3. **JavaScript Integration** (`index.html`): The HTML file imports the generated WebAssembly module and calls the `greet` function.

## Key Files

- **`Cargo.toml`**: Configures the Rust project as a `cdylib` (C-compatible dynamic library) for WebAssembly compilation
- **`src/lib.rs`**: Contains the Rust functions exported to WebAssembly using `wasm-bindgen`
- **`pkg/`**: Generated directory containing the WebAssembly module and JavaScript bindings
- **`index.html`**: Example HTML file demonstrating how to use the WebAssembly module

## Customizing

To add your own functions:

1. Edit `src/lib.rs` and add new functions with the `#[wasm_bindgen]` attribute
2. Rebuild with `wasm-pack build --target web`
3. Update `index.html` to import and use your new functions

## Troubleshooting

- **CORS errors**: Make sure you're serving the files through a local server, not opening the HTML file directly
- **Module not found**: Ensure the `pkg/` directory exists and contains the generated files
- **Build errors**: Check that you have the latest version of Rust and wasm-pack installed

## Learn More

- [Rust and WebAssembly Book](https://rustwasm.github.io/docs/book/)
- [wasm-bindgen Documentation](https://rustwasm.github.io/docs/wasm-bindgen/)
- [WebAssembly MDN Documentation](https://developer.mozilla.org/en-US/docs/WebAssembly)