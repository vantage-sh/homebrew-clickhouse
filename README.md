# Homebrew Tap for ClickHouse (by Altinity)

## Available formulae

```text
clickhouse                       - alias, same as clickhouse@lts
clickhouse-client                - alias, same as clickhouse@lts
clickhouse-server                - alias, same as clickhouse@lts

clickhouse@lts                   - alias, always points to the latest LTS versioned formula (clickhouse@26.8)

clickhouse@26.8                  - the latest release / LTS, version: 26.8.12.53-lts
clickhouse@26.2                  - keg-only, version: 26.2.1.1139-stable
clickhouse@26.1                  - keg-only, version: 26.1.3.52-stable
clickhouse@25.12                 - keg-only, version: 25.12.7.21-stable
clickhouse@25.11                 - keg-only, version: 25.11.9.34-stable
clickhouse@25.10                 - keg-only, version: 25.10.6.36-stable
clickhouse@25.8                  - keg-only, version: 25.8.8.26-lts
clickhouse@25.6                  - keg-only, version: 25.6.8.10-stable
clickhouse@25.4                  - keg-only, version: 25.4.12.9-stable
```

## Quick start: one-liner

```sh
brew install vantage-sh/clickhouse/clickhouse
```

## Quick start: fine control

First, register the tap (needs to be done only once):

```sh
brew tap vantage-sh/clickhouse
```

Then, install the formula you need:

```sh
brew install clickhouse
# ..or
brew install clickhouse@25.4
# ...and so on.
```

Please, always read the `Caveats` sections, which are displayed after the installation, carefully.

Note, that the installation doesn't require `sudo` and will deploy ClickHouse under the standard Homebrew prefix.

## Running ClickHouse server

Do not use `sudo`, ever. Do not start the ClickHouse server manually, instead use `brew services`:

```sh
brew services start clickhouse
# ..or
brew services start clickhouse@25.4
# ...and so on.
```

ClickHouse is deployed under the standard Homebrew prefix. The relevant directories are:

```text
Config:    $(brew --prefix)/etc/clickhouse-server/
Data:      $(brew --prefix)/var/lib/clickhouse/
Logs:      $(brew --prefix)/var/log/clickhouse-server/
PID file:  $(brew --prefix)/var/run/clickhouse-server/
```

These files and directories will be preserved between installations.

Make sure you stop the server, when upgrading the formula.

If you absolutely need to run ClickHouse server manually, the command that corresponds to `brew services start clickhouse` would be:

```sh
$(brew --prefix clickhouse)/bin/clickhouse server --config-file $(brew --prefix)/etc/clickhouse-server/config.xml --pid-file $(brew --prefix)/var/run/clickhouse-server/clickhouse-server.pid
```

## Versioned formulae

All except the latest versioned ClickHouse formulae are configured as [keg-only](https://docs.brew.sh/FAQ#what-does-keg-only-mean), so in order to refer to an executable from such formula you have to provide the full path to it, e.g.:

```sh
$(brew --prefix clickhouse@25.4)/bin/clickhouse client
```

## Pre-built binary packages (bottles)

Bottles for the following platforms are available:

```text
macOS Monterey (version 12) on Intel
macOS Monterey (version 12) on Apple silicon
```

Eventually, this list will be extended to also contain some of the previous versions of macOS.

## Building (the latest versions) from sources

Formulae will be built from sources automatically if the corresponding bottles are not available for your platform.

It could take several hours to build ClickHouse from sources, so you will probably want to monitor the progress. To enable verbose output for that scenario, add `--verbose` to `brew install ...`:

```sh
brew install --verbose clickhouse
```

You can also build the latest version (`HEAD`) of the sources for a formula:

```sh
brew install --HEAD --verbose clickhouse
```

The above command will check out the tip of the branch that corresponds to that specific version (e.g., branch [25.4](https://github.com/ClickHouse/ClickHouse/tree/25.4) for `clickhouse@25.4` and so on) and build it from sources.

## Homebrew on Linux (Linuxbrew)

Building the formulae from this tap is not tested in Linux, and bottles are not available, but there are no known conceptual problems, and they should generally work. Feel free to experiment and report any [issues](https://github.com/Altinity/homebrew-clickhouse/issues).

## Adding or updating formulae in this tap (for maintainers only)

Refer to [Maintenance](MAINTENANCE.md) for instructions.

## Useful links

- [Altinity](https://altinity.com/)
- [ClickHouse](https://clickhouse.com/)
- [Homebrew](https://brew.sh)
