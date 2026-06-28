# Task 1

# Task 2

I created a GitHub Actions workflow for a Vite and TypeScript project. It runs on pushes and pull requests to `main`, as well as manual execution.

The workflow tests the project on Node.js `22.x` and `24.x`, uses npm caching, installs dependencies with `npm ci`, and runs linting, tests, type-checking, and the production build. I also added a CI status badge to the README.

```YAML
name: Portal CI

on:
  pull_request:
    branches:
      - main
  push:
    branches:
      - main
  workflow_dispatch:

permissions:
  contents: read

jobs:
  portal:
    name: Node ${{ matrix.node-version }}
    runs-on: ubuntu-latest

    strategy:
      fail-fast: false
      matrix:
        node-version:
          - 22.x
          - 24.x

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.node-version }}
          cache: npm
          cache-dependency-path: package-lock.json

      - name: Install dependencies
        run: npm ci

      - name: Lint
        run: npm run lint

      - name: Test
        run: npm run test

      # The build includes `tsc --noEmit`.
      - name: Build
        run: npm run build
```

# Task 3

I used act to run the GitHub Actions workflow locally before pushing it:

`act push -W .github/workflows/portal-ci.yml -j portal`

`act` executed the complete Node.js matrix inside Docker. Both Node.js 22.x and 24.x jobs completed successfully, including dependency installation, linting, tests, type-checking, and the production build.

During setup, I initially installed a different program also named `act` using the fedora package manager `dnf`. After replacing it with `nektos/act`, the workflow ran correctly.