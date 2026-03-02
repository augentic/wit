# Omnia WIT Specifications

WIT (WebAssembly Interface Type) package definitions used by the Omnia platform.
Published to the GitHub Container Registry at `ghcr.io/augentic/omnia/<package>`.

## Prerequisites

Install [wkg](https://github.com/bytecodealliance/wasm-pkg-tools).

## Publishing

### Authentication

Authenticate with the GitHub Container Registry using a PAT with `write:packages` scope:

```bash
echo "$GITHUB_TOKEN" | docker login ghcr.io -u USERNAME --password-stdin
```

### Build and publish a package

To publish the otel package to ghcr.io/augentic/omnia/otel:

```bash
wkg wit build --config .config.toml --wit-dir ./otel
wkg publish --config .config.toml omnia:otel@0.1.0.wasm
```

## Using

To fetch a package in another project, add the following to your wasm-pkg config a local `.wkg-config.toml`:

```toml
default_registry = "augentic"

[namespace_registries]
omnia = "omnia.host"
wasi = "wasi.dev"

[package_registry_overrides]
"wasi:blobstore" = "omnia.host"
"wasi:keyvalue" = "omnia.host"
"wasi:messaging" = "omnia.host"
"wasi:sql" = "omnia.host"
```

Then fetch the package:

```bash
wkg get omnia:otel@0.1.0 --config .wkg-config.toml --output ./otel/otel.wit
```

And fetch any dependencies:

```bash
wkg wit fetch --config .config.toml --wit-dir ./otel
```

