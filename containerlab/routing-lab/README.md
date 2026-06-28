# SDN 05 Assignment — 3-Node Containerlab Routing Topology

## Goal

This assignment implements a 3-node Containerlab topology:

hs1 <--> rt1 <--> hs2

hs1 and hs2 are two hosts in different IPv4 and IPv6 subnets. rt1 acts as the router between them.

## Verification

The topology was deployed with:

```bash
./deploy.sh
