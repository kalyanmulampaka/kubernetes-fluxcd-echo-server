## Deploy the echo-server App

### Create the namespace

`kubectl create ns echo-server`

### Create the github access secret
Create the github access secret in Flux

```
flux create secret git github-echo-server-secret \
    -n echo-server \
    --url=ssh://git@github.com/kalyanmulampaka/kubernetes-fluxcd-echo-server.git \
    --private-key-file=.ssh/id_ed25519-kal
```

### Deploy the App
Execute the following to create the GitRepository, Kustomization which installs and manages the HelmRelease in Flux.

`kubectl apply -f deploy-echo-server.yaml`

### Auto-Deployment
Any changes merged to the git source repository will be automatically deployed.
To test this make few changes in Chart.yaml and values.yaml and checkin to git.
Flux will pull the changes and deploy the updated helm chart.
