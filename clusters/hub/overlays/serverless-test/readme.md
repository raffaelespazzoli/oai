# test serverless

```sh
export knative_route_url=$(oc -n knative-serving get route knative -o jsonpath='{.spec.host}')
export serverless_basedomain=${knative_route_url#*.}
curl -k https://showcase-serverless-test.${serverless_basedomain}/hello
```

generate some load

```sh
export knative_route_url=$(oc -n knative-serving get route knative -o jsonpath='{.spec.host}')
export serverless_basedomain=${knative_route_url#*.}
docker run rogerw/cassowary:v0.14.1 -u https://showcase-serverless-test.${serverless_basedomain}/hello -c 10 -n 2400 -d 30
```