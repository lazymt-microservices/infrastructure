### infrastructure
`settings to deploy the project`

### requires

- install [skaffold](https://skaffold.dev/docs/install/) manually
- or via cmd
```shell
choco install -y skaffold
```

- install [helm](https://helm.sh/docs/intro/install/)

- install ingress controller. [Help](https://kubernetes.github.io/ingress-nginx/deploy/#quick-start).
```shell
helm upgrade --install ingress-nginx ingress-nginx \
  --repo https://kubernetes.github.io/ingress-nginx \
  --namespace ingress-nginx --create-namespace
```

- create a secret
```shell
kubectl create secret generic jwt-secret --from-literal=JWT_KEY=asdf
```
- to delete secret if needed
```shell
kubectl delete secret jwt-secret
```

### deploy

#### step 1
- build docker image for auth service. Push not needed for dev.
```shell
cd auth-srv
docker build -t notlazymisha/auth .
docker push notlazymisha/auth #for prod, not needed for dev
```
- start deployment
```shell
cd infrastructure
scaffold dev #./scaffold.exe dev
```
