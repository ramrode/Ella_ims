# Perform a Rolling Upgrade

This guide walks through upgrading every node in a running Ella IMS high-availability cluster, one at a time, without taking the cluster offline.

## Prerequisites

- A running cluster deployed via [Deploy a High Availability Cluster](https://docs.ellanetworks.com/ims/how_to/deploy_ha_cluster/index.md).
- The next version of `ella-ims` available.

## Upgrade the nodes

Repeat these steps for each node.

1. On that host, refresh the snap:

   ```
   sudo snap refresh ella-ims
   ```

1. On the leader's **Cluster** page, wait for the node to return to **Healthy**.

1. Move to the next node.

1. Set the new image:

   ```
   kubectl set image statefulset/ella-ims -n ella ims=ghcr.io/ellanetworks/ella-ims:<version>
   ```

1. Wait for the rollout:

   ```
   kubectl rollout status statefulset/ella-ims -n ella
   ```

## Verify the upgrade

After every node has been upgraded, open the leader's **Cluster** page and confirm:

- Every node's **Version** column shows the target release.
- Every node is **Healthy** and its **Drain** column shows **Active**.
