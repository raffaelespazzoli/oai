# test serverless

```sh
export knative_route_url=$(oc -n knative-serving get route knative -o jsonpath='{.spec.host}')
export serverless_basedomain=${knative_route_url#*.}