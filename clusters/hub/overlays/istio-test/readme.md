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

