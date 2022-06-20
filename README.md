
## Deployment Guide

https://docs.livekit.io/deploy/kubernetes/


## Config

Edit `override.yaml` and fill variables
  - REDIS_HOST
  - REDIS_DB
  - REDIS_USERNAME
  - REDIS_PASSWORD
  - API_KEY
  - API_SECRET
  - TURN_DOMAIN
  - SSL_CERT_SECRET_NAME
  - API_ENDPOINT_URL
  - API_DOMAIN


## Commands
DEPLOYMENT_NAME
 - Staging: `livekit-server-staging`
 - Production: ``



### Install Helm chart

```
helm install -f ./livekit-server/values.yaml -f override.yaml DEPLOYMENT_NAME ./livekit-server
```


### Upgrade Helm chart

```
helm upgrade -f ./livekit-server/values.yaml -f ./override.yaml DEPLOYMENT_NAME ./livekit-server
```
