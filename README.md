# linkerd-kubernetes

Check out the blog post [here](https://medium.com/@jeffzzq/modeling-environments-with-linkerd-ingress-part-1-2-d6f2a8aa48c5)

Most of the information was synthesized from a few linkerd articles ([link](https://blog.buoyant.io/2017/04/06/a-service-mesh-for-kubernetes-part-viii-linkerd-as-an-ingress-controller/), [link](https://blog.buoyant.io/2016/05/04/real-world-microservices-when-services-stop-playing-well-and-start-getting-real/)).

# How to Use

## 1. Create the Cluster

```
$ cd preprod
$ vagrant up
```

## 2. Generate the Manifests

```
$ ENVIRONMENT=preprod ../manifests/calculator-app/generate.sh
```

## 3. Apply the Generated Manifests

```
KUBECONFIG=$PWD/kubeconfig kubectl apply -f ../manifests/calculator-app/templated
```

## 4. Apply the Linkerd Manifest

```
KUBECONFIG=$PWD/kubeconfig kubectl apply -f ../manifests/linkerd/linkerd-ingress.yaml
```

## Linkerd

### Sample Logical Names

These are based on the Ingress Identifier. More more information on Identifiers, see [this link](https://linkerd.io/in-depth/routing/).

```
/svc/my-namespace/my-named-port/my-service
```

### Sample Concrete names

A Pod IP.

```
10.2.0.3
```

## Networks

* Orlando: preprod (/28 [0-15])
* Orlando: prod (/28 [16-31])
* Tokyo: preprod (/28 [32-47])
* Tokyo: prod (/28 [48-63])
