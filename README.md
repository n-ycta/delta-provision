# Delta Provision

Provision a reachable SSH host and keep connection jobs separate from the Web frontend.

Independent headless Delta service. No browser, Web plugin, or graphical session is required. Web, Desktop and Android are optional clients; Android delegates desktop-only operations to a trusted paired desktop/VPS node.

## Install and use

Install **Delta Provision** from the official Delta plugin catalog on the node where this service should run. Compatible Web/native hosts show which optional service dependencies are installed, disabled or incompatible. Installing Web is not required to keep this service running.

For an owner-operated Core CLI installation:

```sh
delta call packages.install --json '{"id":"dev.delta.provision"}'
```

Use the node connection/provisioning workflow in a compatible host. Run preflight/probe before approving installation; review the target, required permissions and SSH trust. A connection job can continue without an open browser. This does not bypass an SSH server policy, supply credentials automatically, open firewall ports or create a general VPN. Use the API below for headless clients.

The supervisor owns service startup. Do not run a second manual copy against an active managed profile. Back up the profile before migration or incompatible upgrades; uninstalling a UI client is not a data backup.

## Runtime

Requires Node.js 22+ and Delta Core >=0.4.3 <0.5.0. Run `npm ci --omit=dev`, then `npm start` with `DELTA_HOME`, `DELTA_URL`, and a service `DELTA_TOKEN`. Executable services are trusted host code, not an OS sandbox.

## API

- `provision.probe`
- `provision.install`
- `provision.status`
- `provision.preflight`
- `provision.connections`
- `provision.remove`

Core authenticates API calls. Forwarded calls retain the original principal through a live, component-bound invocation; the caller is never trusted from JSON arguments. A caller must be authorized for both the compatibility endpoint and the destination capability. Existing owner access is unchanged; narrowly scoped keys may need the new service scopes.

## Data and migration

SSH jobs and connection records retain `DELTA_HOME/data/connections`. Tunnels remain supervised by Core, not a graphical window. SSH credentials are not logged or saved.

## Development and verification

Run `npm ci` and `npm test` in this repository. Direct `npm start` is for a deliberately configured service environment; an ordinary UI client should not receive its service credential.


Automated tests use isolated fixtures. Physical desktop restart, phone lifecycle, and production VPS acceptance are not implied by a passing test suite.
