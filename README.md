### infrastructure
`settings to deploy the project`

### requires

- install Docker Desktop for Windows / Mac

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
- build docker image for auth service
```shell
cd auth-srv
docker build -t notlazymisha/auth .
docker push notlazymisha/auth
```
- build docker image for the client
```shell
cd client
docker build -t notlazymisha/client .
docker push notlazymisha/client
```

#### step 2
- start deployment
```shell
cd infrastructure
scaffold dev #./scaffold.exe dev
```

#### result
- GET request to the `/api/users/currentuser` returns
```json
{
    "currentUser": null
}
```
