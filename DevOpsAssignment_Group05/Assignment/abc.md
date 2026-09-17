# NPM as a Build Automation Tool

## 1. Overview & Core Concept
While originally designed as Node's package manager, npm functions as a lightweight task runner and build automation tool through its `scripts` property in `package.json`. It eliminates the need for separate task runners like Gulp or Grunt by executing commands directly in the system shell while providing automatic access to locally installed binaries in `node_modules/.bin`.

---

## 2. Key Components in DevOps

* **Dependency Segregation:**
  * `dependencies`: Production packages required at runtime.
  * `devDependencies`: Build-time utilities, compilers, bundlers, and testing frameworks (e.g., Babel, Webpack, ESLint, Jest).
* **Build Lifecycle Hooks:**
  * Scripts prefixed with `pre` run automatically before the target script (e.g., `prebuild` runs before `build`).
  * Scripts prefixed with `post` run automatically after a successful exit code (e.g., `postbuild` runs after `build`).
* **Task Chaining:**
  * `&&` executes tasks sequentially, halting on the first non-zero exit code.
  * `&` runs tasks concurrently (or use tools like `concurrently` for cross-platform support).

---

## 3. Sample `package.json` Configuration

```json
{
  "name": "devops-sample-app",
  "version": "1.0.0",
  "description": "DevOps automated build pipeline example",
  "main": "dist/index.js",
  "scripts": {
    "clean": "rm -rf dist",
    "lint": "eslint src/**/*.js",
    "prebuild": "npm run clean && npm run lint",
    "build": "babel src -d dist --copy-files",
    "postbuild": "echo 'Build completed successfully!'",
    "test": "jest --ci",
    "start": "node dist/index.js"
  },
  "devDependencies": {
    "@babel/cli": "^7.24.0",
    "@babel/core": "^7.24.0",
    "eslint": "^8.57.0",
    "jest": "^29.7.0"
  },
  "dependencies": {
    "express": "^4.19.0"
  }
}
