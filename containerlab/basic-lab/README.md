# SDN 04 Homework — Bind-Mount Entrypoint in ContainerLab

## Objective

The goal of this homework is to modify the `basic-lab` Containerlab topology so that the entrypoint script is not copied into the Docker image. Instead, the script is bind-mounted from the host at runtime.

## Changes Made

1. Removed the `COPY` instruction for `bin/entrypoint.sh` from the `Dockerfile`.
2. Added a bind mount in `basic-lab.clab.yml` so that:

```yaml
./bin/entrypoint.sh:/entrypoint.sh:ro
```

is mounted inside each container.

3. Kept the `exec` directive unchanged:

```yaml
exec:
  - bash /entrypoint.sh
```

4. Kept the node configuration files mounted as read-only files:

```yaml
configs/node1.cfg:/etc/nodes/node1.cfg:ro
configs/node2.cfg:/etc/nodes/node2.cfg:ro
```

## Verification

The lab was deployed successfully using:

```bash
./deploy.sh
```

The containers were running correctly:

```bash
sudo docker ps
```

IPv4 connectivity was verified with:

```bash
sudo docker exec -it clab-basic-lab-node1 ping -c 3 10.0.0.2
sudo docker exec -it clab-basic-lab-node2 ping -c 3 10.0.0.1
```

IPv6 connectivity was verified with:

```bash
sudo docker exec -it clab-basic-lab-node1 ping -c 3 fc00::2
sudo docker exec -it clab-basic-lab-node2 ping -c 3 fc00::1
```

Both IPv4 and IPv6 pings completed successfully with `0% packet loss`.

## Result

The entrypoint script is now provided through a host bind mount instead of being copied into the Docker image, and the lab still works correctly.

