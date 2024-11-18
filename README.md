# wasm_pi

Rust WebAssembly first steps

## Step-by-step walkthrough

1. Install `wasm-pack`, the high-level build tool for Rust WebAssembly projects.

    ```sh
    cargo install wasm-pack
    ```

2. Create a new project with a library create. Here, we are using `cargo new`, but for more sophisticated Wasm project you may want to use `wasm-pack new`.

    ```sh
    cargo new --lib wasm_add
    ```

3. Add `wasm-bindgen` as a dependecy.

    ```sh
    cd wasm_add
    cargo add wasm-bindgen
    ```

4. Open the project in your code editor and modify `Cargo.toml` to change the library `crate-type` to `cdylib`:

    ```toml
    ...
    [lib]
    crate-type = ["cdylib"]
    ...
    ```

5. Change the initial `src/lib.rs` code:

    ```rust
    use wasm_bindgen::prelude::*;

    #[wasm_bindgen]
    pub fn add(a: i32, b: i32) -> i32 {
        a + b
    }
    ```

6. Build the project with `wasm-pack` (`web` target, ES6 module)

    ```sh
    wasm-pack build --target web
    ```

7. Add `index.html` file to the project root with the following contents:

    ```html
    <!doctype html>
    <html lang="en-US">
    <head>
        <meta charset="utf-8" />
        <title>Wasm Add</title>
    </head>
    <body>
        <script type="module">
        import init, { add } from "./pkg/wasm_add.js";
        init().then(() => {
            const a = 7;
            const b = 13;
            const x = add(a, b);
            document.body.textContent = `${a} + ${b} = ${x}`;
        });
        </script>
    </body>
    </html>
    ```

8. Install a simple web server (Host These Things Please), and serve the project root folder, than visit the local page

    ```sh
    cargo install cargo install https
    http
    ```
