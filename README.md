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
- set NODE_ENV

macOS / OS X or Linux:
```shell
export NODE_ENV=dev
```
Windows:
```shell
SET NODE_ENV=dev
```
### deploy

#### step 1
- build docker image for auth service
```shell
cd auth-srv
docker build -t YOURDOCKERID/auth .
docker push YOURDOCKERID/auth
```
- build docker image for the client
```shell
cd client
docker build -t YOURDOCKERID/client .
docker push YOURDOCKERID/client
```

#### step 2
- start deployment
```shell
cd infrastructure
scaffold dev #./scaffold.exe dev
```

#### result
Give `skaffold` a little time to start up. 
You should then be able to access the app in your browser at `kubernetes.docker.internal`

- Postman:
- GET request to the `/api/users/currentuser` returns
```json
{
    "currentUser": null
}
```
