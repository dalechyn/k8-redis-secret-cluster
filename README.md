# k8-parrot-redis

Scalable kubernetes redis cluster.

## Steps:
1. Create a separate namespace to isolate redis components:
   ```
   kubectl create ns redis
   ```
2. Create a *Secret* and call it `redis-secret` with `REDIS_PASSWORD` in it:
   ```
   kubectl -n redis create secret generic redis-secret \
   --from-literal=REDIS_PASSWORD=$(echo -n your_secret_password | base64)
   ```
3. Apply Redis ConfigMap:
   ```
   kubectl -n redis apply -f kubernetes/config/redis-configmap.yaml
   ```
4. Apply Redis StatefulSet (change amount of replicas if needed, default is 3):
   ```
   kubectl -n redis apply -f kubernetes/config/redis-statefulset.yaml
   ```
5. Apply Sentinel StatefulSet (amount of replicas has to be greater than 3):
   ```
   kubectl -n redis apply -f kubernetes/config/sentinel-statefulset.yaml
   ```
