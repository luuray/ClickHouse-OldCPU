# ClickHouse OldCPU

Unofficial ClickHouse LTS builds for older `x86_64` processors.

> Automated builds are currently paused. The GitHub-hosted workflow was removed because a clean ClickHouse build exceeded the practical capacity of the standard runner. Builds will resume on a higher-performance host.

The build configuration targets the newest published LTS tag with `X86_ARCH_LEVEL=2`. The resulting binary requires the `x86-64-v2` baseline (SSE4.2, SSSE3 and POPCNT), but does not require AVX or AVX2.

## Downloads

Each successfully verified version is published as:

- A self-extracting `clickhouse` binary in [GitHub Releases](https://github.com/luuray/ClickHouse-OldCPU/releases).
- A `linux/amd64` ClickHouse Server image at `ghcr.io/luuray/clickhouse-oldcpu`.

Available container tags include the full upstream version, the LTS series, `lts`, and `latest`.

```bash
docker pull ghcr.io/luuray/clickhouse-oldcpu:latest
docker run -d --name clickhouse-oldcpu \
    -p 8123:8123 -p 9000:9000 \
    ghcr.io/luuray/clickhouse-oldcpu:latest
```

## Verification

Before publication, the workflow:

1. Confirms that CMake configured `X86_ARCH_LEVEL=2`.
2. Runs `clickhouse local` natively.
3. Runs the unbundled binary through QEMU with a Westmere CPU model, which has no AVX or AVX2.
4. Starts the final Server image and executes a query through `clickhouse client`.
5. Publishes a SHA256 checksum, container SBOM, and build provenance.

The release process fails closed: no GitHub Release should be created unless compilation, compatibility checks, container tests, GHCR publication, and anonymous GHCR access all succeed.

## Upstream

ClickHouse is licensed under the Apache License 2.0. Source releases are fetched directly from [ClickHouse/ClickHouse](https://github.com/ClickHouse/ClickHouse).
