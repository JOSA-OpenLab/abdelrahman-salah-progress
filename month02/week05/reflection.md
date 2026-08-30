# Task 1

For this task, I scouted for a small missing test case in the [uutils/grep](https://github.com/uutils/grep) repository. I focused on behavior that was already implemented but did not appear to have direct regression coverage.

I found that `-Z / --null` was tested with `filename-list` output using `-l`, but not with normal filename-prefixed matching output. This is a separate output path, so I prepared a focused test for it.

The added test checks that:

`grep -Z -H x f`

prints a NUL byte between the filename and the matched line.

The test I prepared was:
```rust
#[test]
fn null_separator_applies_to_normal_filename_prefixes() {
    let (scene, mut c) = ucmd();
    scene.fixtures.write("f", "x\n");
    c.args(&["-Z", "-H", "x", "f"])
        .succeeds()
        .stdout_is_bytes(b"f\0x\n");
}
```
This follows the Arrange / Act / Assert structure:

Arrange: create the test fixture file f.
Act: run grep with -Z -H x f.
Assert: verify success and exact byte output.

I verified the behavior against GNU grep 3.12 and confirmed both produced the same bytes. I also verified that the test is meaningful by intentionally changing the expected output from a NUL byte to :, which caused the test to fail.

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
