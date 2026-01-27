# Grape — Commands and Usage

This repository contains the Grape node/application. This README documents the available command-line flags and provides examples to run multiple nodes locally.

## Quick examples

Run two local nodes that connect to each other as bootstrap peers:

````markdown name=README.md
```bash
grape --dp 20001 --aph 30001 --bn '127.0.0.1:20002'
grape --dp 20002 --aph 40001 --bn '127.0.0.1:20001'
```
````

Replace the ports and addresses as needed for your environment.

## Command-line flags

- `--dp <port>` — data port for peer-to-peer data connections. Use a unique port for each node when running multiple nodes on the same machine.
- `--aph <port>` — API/HTTP port for the node's admin or HTTP API (exposed services).
- `--bn '<host:port>'` — bootstrap node address (a comma-separated list is usually supported). Point this at one or more already-running nodes so they can discover each other.

Note: The meanings above are inferred from common naming; adjust them to match the implementation in your code if the flags are different.

## Running multiple nodes locally

1. Make sure the ports you choose are free.
2. Start the first node (example uses 20001 for dp and 30001 for aph):

```bash
grape --dp 20001 --aph 30001 --bn '127.0.0.1:20002'
```

3. Start the second node and point it to the first as bootstrap:

```bash
grape --dp 20002 --aph 40001 --bn '127.0.0.1:20001'
```

4. Check logs or the API endpoints to verify the nodes discovered each other.

## Examples

- Start a standalone node:

```bash
grape --dp 20001 --aph 30001
```

- Start a node and connect to multiple bootstraps:

```bash
grape --dp 20003 --aph 30003 --bn '127.0.0.1:20001,127.0.0.1:20002'
```

## Troubleshooting

- If nodes do not connect, ensure firewalls are disabled for the ports, and the addresses/ports in `--bn` are reachable.
- If ports are already in use, pick different ports or stop the process using them (on Linux/macOS: `lsof -i :<port>`).

## Contributing

If you edit or add commands in the repository, please update this README to reflect the correct flag names and their meanings. If you're unsure what a flag does, search the code for flag registration (e.g., `flag`, `cobra`, or argument parsing code) and update this documentation accordingly.

## License

Include license information here if applicable.
