- CRA was go-to-tool for a long time but we see increased development and build time when the project size increases. This slow feedback loop affects dev's productivity and happiness.

- <strong>Unlike CRA, Vite doesn't build your entire application before serving, instead it builts the application on demand. <u>It also leverages the power of native ES Modules, esbuild and Rollup to improve the dev and build time</u></strong>

#### 1. Why is CRA slow?

- CRA uses Webpack under the hood.
- <strong>The webpack bundles the entire application code before it can be served.</strong>
- With a large codebase, it takes more time to spin up the dev server and reflecting the changes takes a long time
- <u>All the code must be bundled in order to start a bundle-based dev server.</u>

#### 2. What is Vite?

- next gen tool that focuses on speed and performance

<strong>It consists of two major parts</strong>

##### 1. A dev server that provides rich feature enhancements over native ES modules: fast Hot Module Replacement (HMR), pre-bundling, support for typescript, jsx, and dynamic import.

##### 2. A build command that bundles your code with Rollup, pre-configured to output optimized static assets for production.

---

#### 3. Why prefer Vite over create-react-app?

##### 1. Faster spin-up of the dev server
- Unlike CRA or bundler-based build setup, Vite does not build the entire application before serving. 

- It divides the application modules into two categories