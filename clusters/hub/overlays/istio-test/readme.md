# Test

run:

```sh
export GATEWAY_URL=$(oc -n istio-system get route istio-ingressgateway -o jsonpath='{.spec.host}')
curl -kv ${GATEWAY_URL}/productpage
```