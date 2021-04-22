## Helper Commands

### Create `ImagePullSecrets` with JSON service account

```
kubectl create secret docker-registry \
sourcecode-gcr-pull-secret \
--namespace=kolpotoru-prod \
--docker-server=gcr.io \
--docker-username=_json_key \
--docker-password="$(cat ~/Desktop/permission-to-gcr-service-account.json)" \
--docker-email=rafikfarhad@gmail.com

```

## Helper Resource

### Expose TCP port from cluster

- Create configmap name `tcp-services`
  ```
    apiVersion: v1
    kind: ConfigMap
    metadata:
    name: tcp-services
    namespace: ingress-nginx
    data:
      3306: kolpotoru-prod/mysql-service:3306
  ```

- Update deployment `ingress-nginx-controller` and add args: `--configmap=$(POD_NAMESPACE)/ingress-nginx-controller`
  
  Command: `kubectl edit --namespace ingress-nginx deployments.apps ingress-nginx-controller`

- Update service `ingress-nginx-controller` and add to ports[]: 
   ```
   - name: https
     port: 3306
     targetPort: 3306
     protocol: TCP
    ```
  
  Command: `kubectl edit --namespace ingress-nginx service ingress-nginx-controller`

  - [Ref 1](https://github.com/kubernetes/ingress-nginx/blob/master/docs/user-guide/exposing-tcp-udp-services.md)
  - [Ref 2](https://chrisedrego.medium.com/setting-up-a-standalone-mysql-instance-on-kubernetes-exposing-it-using-nginx-ingress-controller-262fc7af593a)