# Unkey CLI

This repository hosts the release builds of `unkey`, the command-line tool for [Unkey](https://www.unkey.com). Use `unkey` to manage projects, deployments, API keys, and other Unkey resources from your terminal.

The source code is not in this repository. The release workflow in Unkey's main repository builds each release and publishes it here.

## Install the CLI

The CLI is a single binary for macOS and Linux, on both x86_64 and arm64. There is no Windows build.

To install with Node.js, use npm:

```bash
npm install -g unkey
```

The npm package downloads the binary for your platform from this repository's releases during the install.

To install without Node.js, download the archive for your platform and put the `unkey` binary on your `PATH`. This example installs the latest release on an Apple silicon Mac:

```bash
curl -fsSLO https://github.com/unkeyed/cli/releases/latest/download/unkey_Darwin_arm64.tar.gz
tar -xzf unkey_Darwin_arm64.tar.gz unkey
sudo mv unkey /usr/local/bin/
```

For other platforms, replace the archive name:

| Platform | Archive |
| --- | --- |
| macOS, Apple silicon | `unkey_Darwin_arm64.tar.gz` |
| macOS, Intel | `unkey_Darwin_x86_64.tar.gz` |
| Linux, x86_64 | `unkey_Linux_x86_64.tar.gz` |
| Linux, arm64 | `unkey_Linux_arm64.tar.gz` |

To check the installation, print the version:

```bash
unkey --version
```

## Verify a download

Each release has a file named `unkey_<version>_checksums.txt` with the SHA-256 sum of each archive. To check an archive, download the checksum file from the same release and compare. Set `VERSION` to the release you downloaded:

```bash
VERSION=2.0.157
curl -fsSLO "https://github.com/unkeyed/cli/releases/download/cli%2Fv${VERSION}/unkey_${VERSION}_checksums.txt"
grep unkey_Darwin_arm64.tar.gz "unkey_${VERSION}_checksums.txt" | shasum -a 256 -c
```

The last command prints `unkey_Darwin_arm64.tar.gz: OK` when the archive matches.

## Sign in and run a command

```bash
unkey login
unkey projects list
```

`unkey login` signs you in through the browser and stores a session in the system keychain. In CI, set the `UNKEY_ROOT_KEY` environment variable instead. `unkey --help` lists every command.

The CLI is early. Commands, flags, and output can change between releases. For scripts that must not break, call the Unkey HTTP API directly.

## Read the documentation

- [Install the CLI](https://www.unkey.com/docs/platform/cli/install)
- [The unkey CLI](https://www.unkey.com/docs/platform/cli/overview), with a page for each command group
- [CLI authentication](https://www.unkey.com/docs/platform/cli/authentication)
- [CLI output and shared flags](https://www.unkey.com/docs/platform/cli/output-and-flags)

## Releases and versions

Release tags have the form `cli/vX.Y.Z`. Stable releases get the npm tag `latest`. Pre-releases get the npm tag `next`:

```bash
npm install -g unkey@next
```

## Report a problem

Open an issue in this repository. Include the output of `unkey --version` and the command that failed. Add `--debug` to the command to print the request ID, and include that ID too. Never paste a root key or a session token into an issue.
