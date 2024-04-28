# Test

run:

```sh
export GATEWAY_URL=$(oc -n istio-test get route istio-test -o jsonpath='{.spec.host}')
curl -kv ${GATEWAY_URL}/productpage
```