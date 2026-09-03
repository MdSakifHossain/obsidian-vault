# Docker Networking

## Containers are isolated

A Docker container has its own network namespace.

Inside a container:

- `localhost` refers to the container itself.
- It does NOT refer to the host machine.

## Connecting a container to a host service

If a service runs on the host, the container must reach it through the host.

Example:

```text
Host
└── Ollama (11434)

Container
└── Open WebUI (8080)
```

Run the container with:

```bash
--add-host=host.docker.internal:host-gateway
```

Then connect to:

```text
http://host.docker.internal:11434
```

instead of

```text
http://localhost:11434
```

## Common problem

If the host service only listens on:

127.0.0.1

the container cannot connect.

The service must listen on:

0.0.0.0

or

*