# Threat model

## What this project does and where untrusted input enters
A system metrics exporter (Go, Prometheus node_exporter). Untrusted input: data read from the
host (procfs, sysfs, filesystems) and the HTTP endpoint it serves. Parsing of host metrics and
the collector plugins are the main surfaces.

## Components that matter most / least
- most: the collector plugins that parse host data and the HTTP endpoint.
- less: the docs, tooling.

## How to exercise it
Run it against crafted procfs-like inputs (where possible); exercise the HTTP endpoint.

## How you rate severity
- RCE or auth bypass: critical. Parser bugs: high. DoS: medium.

## Anything to leave alone
- Vendored third-party modules are lower priority than the project code.
