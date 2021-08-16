# Running in Kubernetes

This demo assumes usage of [Kubernetes running via Docker Desktop](https://www.docker.com/products/kubernetes). This simplified environment has the benefit of using a shared Docker daemon between your machine and Kubernetes, meaning there's no need to manage or configure an alternate Docker registry.

## How-to

### Install Istio (_optional_)

```sh
$ curl -L https://istio.io/downloadIstio | ISTIO_VERSION=1.11.0 sh -
$ export ISTIO_HOME=$PWD/istio-1.11.0
$ export PATH=$ISTIO_HOME/bin:$PATH
$ istioctl install -y
```

### Install and run Kiali (_optional_)

```sh
$ kubectl apply -f $ISTIO_HOME/samples/addons/prometheus.yaml
$ kubectl apply -f $ISTIO_HOME/samples/addons/kiali.yaml
$ istioctl dashboard kiali
```

### Build and run the Spring Pet Clinic

```sh
$ ./mvnw spring-boot:build-image
$ kubectl apply -f kubernetes/petclinic.yml
$ echo "\nSpring Pet Clinic is available at http://localhost:$(kubectl get service gateway --namespace spring-petclinic -o go-template='{{range.spec.ports}}{{.nodePort}}{{end}}')"
```

### Build and reload a single service (_development_)

```sh
$ ./mvnw -DskipTests -pl spring-petclinic-api-gateway spring-boot:build-image \
  && kubectl rollout restart deployment gateway --namespace spring-petclinic
```
