# Week07

## task 1

For task 1, I added a dependabot configuration to a fastAPI project, here is the config file:

```yaml
version: 2

updates:
  - package-ecosystem: "uv"
    directory: "/"
    schedule:
      interval: "weekly"
    open-pull-requests-limit: 10

  - package-ecosystem: "docker"
    directory: "/"
    schedule:
      interval: "weekly"
    open-pull-requests-limit: 10

  - package-ecosystem: "github-actions"
    directory: "/"
    schedule:
      interval: "weekly"
    open-pull-requests-limit: 10

```

I am using uv as a package manager for python, and I added docker and github-actions to the config file to keep them up to date as well. I also set the schedule to weekly and limited the number of open pull requests to 10.

after running it for the first time, I got a lot of pull requests for multiple dependencies, so I had to merge them and make my project more secure. I also learned that dependabot can be configured to ignore certain dependencies or versions, which can be useful if you want to avoid breaking changes.

## task 2

for this task I used my [libft project](https://github.com/Abusalah0/libft_42/releases/tag/v1.0.0) which is a C library that I created for my 42 school projects. It has a makefile that generates a static library which can be used in other C projects. I tagged the last commit with a version number and created a release on GitHub. then signed the artifacts with cosign and uploaded them to the release page.

then I verified the signature of the artifacts using cosign with this command:

```bash
cosign verify-blob \
  --bundle libft_42-v1.0.0.tar.gz.sigstore.json \
  --certificate-identity '109g83@gmail.com' \
  --certificate-oidc-issuer 'https://github.com/login/oauth' \
  libft_42-v1.0.0.tar.gz
```

## task 3

I ran syft against a FastAPI project to generate a Software Bill of Materials then I used grype to scan the SBOM for vulnerabilities. grype found a dozen of vulnerabilities in the dependencies, but the highest risk one was a  medium severity vulnerability in the `starlette` package, which is `GHSA-86qp-5c8j-p5mr` also tracked as `CVE-2026-48710`, It stems from missing Host header validation, which allows attackers to send malformed requests that poison `request.url.path`. This discrepancy enables attackers to bypass path-based security controls and access restricted endpoints.

## task 4
