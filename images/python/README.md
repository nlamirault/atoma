# python

Minimal Python runtime image based on [Wolfi OS](https://wolfi.dev/), suitable
for scripting pipelines and CI/CD automation.

## Included Tools

- **Python 3.13** - Python interpreter
- **pip** (`py3-pip`) - Python package installer
- **uv** - Fast Python package and project manager

## Versions

| 📌 Version | ⬇️ Pull URL                                      |
| ---------- | ----------------------------------------------- |
| latest     | ghcr.io/nlamirault/atoma/python:latest      |
| latest-dev | ghcr.io/nlamirault/atoma/python:latest-dev  |

## ✅ Verify the Build Provenance

GitHub CLI ([gh](https://cli.github.com/)) can be used to retrieve the build
provenance, which details the exact commit, workflow, and runner that produced
the image:

- **Production image**

```shell
gh attestation verify \
  --owner nlamirault \
  oci://ghcr.io/nlamirault/atoma/python:latest
```

- **Dev image**

```shell
gh attestation verify \
  --owner nlamirault \
  oci://ghcr.io/nlamirault/atoma/python:latest-dev
```

### Using Cosign

- **Production image**

```shell
cosign verify-attestation \
  --type slsaprovenance \
  --certificate-oidc-issuer https://token.actions.githubusercontent.com \
  --certificate-identity-regexp '^https://github.com/slsa-framework/slsa-github-generator/.github/workflows/generator_container_slsa3.yml@refs/tags/v[0-9]+.[0-9]+.[0-9]+$' \
  ghcr.io/nlamirault/atoma/python:latest@sha256:xxxxxx
```

- **Dev image**

```shell
cosign verify-attestation \
  --type slsaprovenance \
  --certificate-oidc-issuer https://token.actions.githubusercontent.com \
  --certificate-identity-regexp '^https://github.com/slsa-framework/slsa-github-generator/.github/workflows/generator_container_slsa3.yml@refs/tags/v[0-9]+.[0-9]+.[0-9]+$' \
  ghcr.io/nlamirault/atoma/python:latest-dev@sha256:xxxxxx
```

## ✅ Verify the Image Signature

All official images are **cryptographically signed** using
[Sigstore Cosign](https://www.sigstore.dev/).

- **Production image**

```shell
cosign verify \
  --certificate-oidc-issuer=https://token.actions.githubusercontent.com \
  --certificate-identity=https://github.com/nlamirault/atoma/.github/workflows/python.yaml@refs/heads/main \
  ghcr.io/nlamirault/atoma/python:latest | jq
```

- **Dev image**

```shell
cosign verify \
  --certificate-oidc-issuer=https://token.actions.githubusercontent.com \
  --certificate-identity=https://github.com/nlamirault/atoma/.github/workflows/release.yaml@refs/heads/main \
  ghcr.io/nlamirault/atoma/python:latest-dev | jq
```

## ✅ Verify the Image Attestations

- **Production image**

```shell
cosign verify-attestation \
  --type=https://spdx.dev/Document \
  --certificate-oidc-issuer=https://token.actions.githubusercontent.com \
  --certificate-identity=https://github.com/nlamirault/atoma/.github/workflows/release.yaml@refs/heads/main \
  ghcr.io/nlamirault/atoma/python:latest
```

## 📦 Download the Image SBOM Attestations

```shell
cosign download attestation \
  --platform=linux/amd64 \
  --predicate-type=https://spdx.dev/Document \
  ghcr.io/nlamirault/atoma/python:latest | jq -r .payload | base64 -d | jq .predicate
```
