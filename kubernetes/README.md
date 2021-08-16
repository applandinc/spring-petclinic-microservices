## How-to

### Install Istio

```sh
$ curl -L https://istio.io/downloadIstio | ISTIO_VERSION=1.11.0 sh -
$ export ISTIO_HOME=$PWD/istio-1.11.0
$ export PATH=$ISTIO_HOME/bin:$PATH
$ istioctl install -y
```

### Install and run Kiali

```sh
$ kubectl apply -f $ISTIO_HOME/samples/addons/kiali.yaml
$ istioctl dashboard kiali
```

### Install Helm

```sh
$ https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash
```

### Run the Spring Pet Clinic

```sh
$ kubectl apply -f kubernetes/petclinic.yml
```
