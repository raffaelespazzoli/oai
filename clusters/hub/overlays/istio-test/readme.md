# Test

run:

```sh
export GATEWAY_URL=$(oc -n istio-test get route istio-test -o jsonpath='{.spec.host}')
curl -kv ${GATEWAY_URL}/productpage
```

generate some load

```sh
docker run rogerw/cassowary:v0.14.1 -u https://${GATEWAY_URL}/productpage -c 10 -n 2400 -d 30
```

verify that metrics where collected

```sh
export cluster_base_domain=$(oc get ingress.config.openshift.io cluster --template={{.spec.domain}} | sed -e "s/^apps.//")

crome https://grafana.apps.${cluster_base_domain}/d/UbsSZTDik/istio-workload-dashboard?orgId=1&refresh=1m&var-datasource=default&var-namespace=istio-test&var-workload=details-v1&var-qrep=destination&var-srcns=All&var-srcwl=All&var-dstsvc=All
```

verify that traces were collected
