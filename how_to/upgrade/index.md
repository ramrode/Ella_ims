# Upgrade

## Upgrade a standalone node

Refresh the snap:

```
sudo snap refresh ella-ims
```

In the directory of `docker-compose.yaml`, pull the new image and restart the container:

```
docker compose pull
docker compose up -d
```

1. Set the new image:

   ```
   kubectl set image statefulset/ella-ims -n ella ims=ghcr.io/ellanetworks/ella-ims:<version>
   ```

1. Wait for the rollout:

   ```
   kubectl rollout status statefulset/ella-ims -n ella
   ```

1. Open the UI and API on your machine:

   ```
   kubectl port-forward -n ella svc/ella-ims 5020:5020
   ```

Check the running version in the UI's top bar.

## Upgrade a cluster

See [Perform a Rolling Upgrade](https://docs.ellanetworks.com/ims/how_to/rolling_upgrade/index.md).
