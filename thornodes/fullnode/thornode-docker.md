---
description: Setting up a fullnode with Docker
---

# Thornode on Docker

{% hint style="info" %}
The steps shown here are tested on `Ubuntu 24.04`, different distributions may need adjustments to the commands.

All commands are meant to be run as root user, if not specified otherwise. Depending on the server installation, they may need to be run from a different user via `sudo`.
{% endhint %}

## Prerequisites

Install all packages needed for running and configuring the THORNode container

```sh
apt install -y --no-install-recommends aria2 curl docker.io jq pv
```

## Configuration

### Work directory

Prepare work directory

```sh
mkdir -p /opt/thornode/.thornode/config
```

### Genesis

For joining the network, the correct genesis file is required.

{% hint style="warning" %}
Nine Realms infrastructure has been decommissioned. Refer to the upstream [node-launcher documentation](https://gitlab.com/thorchain/devops/node-launcher/-/tree/master/docs) for the current genesis file source.
{% endhint %}

### Sync

The fastest way to join the network is by downloading a current snapshot and syncing from it.

{% hint style="warning" %}
Nine Realms infrastructure has been decommissioned. Refer to the upstream [Thornode Snapshot Recovery and Storage Management](https://gitlab.com/thorchain/devops/node-launcher/-/blob/master/docs/Thornode-Snapshot-Recovery-and-Storage-Management.md) doc for the current snapshot source and recovery procedure.
{% endhint %}

## Start

Start the thornode container

```sh
docker run -d --restart=on-failure \
  -v /opt/thornode/.thornode:/root/.thornode \
  -e CHAIN_ID=thorchain-1 \
  -p 127.0.0.1:1317:1317 \
  -p 127.0.0.1:27147:27147 \
  -p 27146:27146 \
  --name thornode \
  registry.gitlab.com/thorchain/thornode:mainnet-2.135.1 
```
