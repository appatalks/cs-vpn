> [!CAUTION]
> Not ready for production use.

> [!NOTE]
> This extension aims to have similar functionality as described in this no longer maintained GH CLI [Extension](https://docs.github.com/en/codespaces/developing-in-a-codespace/connecting-to-a-private-network#using-the-github-cli-extension-to-access-remote-resources):
>
> `.. allows you to create a bridge between a codespace and your local machine, so that the codespace can access any remote resource that is accessible from your machine. The codespace uses your local machine as a network gateway to reach those resources.`

# cs-vpn
### GitHub Cli Extension: Gateway-Proxy/VPN for Codespaces
<br>


Route select internet traffic through GitHub Codespaces using `sshuttle`, and optionally set up SSH reverse tunnels so the Codespace can access services on your local machine.

## Installation

```bash
gh extension install appatalks/cs-vpn
```

## Usage

```bash
gh codespaces proxy <codespace-name> [flags]
```

## Flags

`--all`             Route all traffic (0.0.0.0/0) through the Codespace

`--only-443`        Route only HTTPS/TLS traffic (0.0.0.0/0:443)

`--dns`             Include DNS queries in the tunnel

`--domains "..."`  Route HTTPS traffic for specific domains (space-separated list)

`--gateway`         Set up a reverse SSH tunnel so the Codespace can reach your localhost (default local:8000 → remote:9000)

`-h`, `--help`      Show usage

## Examples

1. Route only TLS + DNS:
  ```bash
  gh codespaces proxy my-codespace --only-443 --dns
  ```

2. Route GitHub domains + set up local gateway:
  ```bash
  gh codespaces proxy my-codespace --domains "github.com api.github.com" --gateway
  ```

3. Route all traffic:
  ```bash
  gh codespaces proxy my-codespace --all
  ```

4. Custom local port mapping (use env vars before running):
  ```bash
  export LOCAL_PORT=3000 REMOTE_PORT=9001
  gh codespaces proxy my-codespace --gateway
  ```
