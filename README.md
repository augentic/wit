# Omnia WIT Specifications

WIT (WebAssembly Interface Type) package definitions used by the Omnia platform.
Published to the GitHub Container Registry at `ghcr.io/augentic/omnia/<package>`.

## Packages

| Package | Version | OCI Location |
| ------- | ------- | ------------ |
| `wasi:blobstore` | `0.2.0-draft` | `ghcr.io/augentic/wasi/blobstore` |
| `wasi:keyvalue` | `0.2.0-draft2` | `ghcr.io/augentic/wasi/keyvalue` |
| `wasi:messaging` | `0.2.0-draft` | `ghcr.io/augentic/wasi/messaging` |
| `wasi:sql` | `0.2.0-draft` | `ghcr.io/augentic/wasi/sql` |
| `omnia:identity` | `0.1.0` | `ghcr.io/augentic/omnia/identity` |
| `omnia:otel` | `0.1.0` | `ghcr.io/augentic/omnia/otel` |
| `omnia:vault` | `0.1.0` | `ghcr.io/augentic/omnia/vault` |
| `omnia:websocket` | `0.1.0` | `ghcr.io/augentic/omnia/websocket` |

## Prerequisites

Install [wkg](https://github.com/bytecodealliance/wasm-pkg-tools).

## Using a Package

To fetch these packages in another project, add the following to your wasm-pkg config
(`~/.config/wasm-pkg/config.toml` or a local `.config.toml`):

```toml
[package_registry_overrides]
"wasi:blobstore" = { registry = "augentic", metadata = { preferredProtocol = "oci", "oci" = { registry = "ghcr.io", namespacePrefix = "augentic/" } } }
# repeat for each package you need
```

Then fetch:

```bash
wkg get wasi:io@0.2.10
```

## Publishing

### Authentication

Authenticate with the GitHub Container Registry using a PAT with `write:packages` scope:

```bash
echo "$GITHUB_TOKEN" | docker login ghcr.io -u USERNAME --password-stdin
```

### Build and publish a WIT specification

For example, to publish the identity package to ghcr.io/augentic/omnia/identity:

```bash
wkg wit fetch --config .config.toml --wit-dir ./otel
```

```bash
wkg wit build --config .config.toml --wit-dir ./otel
wkg publish --config .config.toml omnia:otel@0.1.0.wasm
```

### Download a WIT specification

For example, to get the otel package:

```bash
wkg get --config .config.toml omnia:otel@0.1.0
```

