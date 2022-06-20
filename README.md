
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

## Setup howlerssl secret
  - Run command
    ```
    $ mkdir howlerssl-certs && cd howlerssl-certs
    ```
  - Replace `TURN_DOMAIN` and `API_DOMAIN`
    ```
    $ certbot certonly \
        --manual \
        --preferred-challenges=dns \
        --email tech@graphy.com \
        --agree-tos \
        --config-dir ./config \
        --logs-dir ./logs \
        --work-dir ./workdir \
        -d API_DOMAIN \
        -d TURN_DOMAIN
    ```
  - Verify acme challenge

## DO - Nginx Ingress

Follow Step 2 and 4 of https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nginx-ingress-on-digitalocean-kubernetes-using-helm

  - ### Install Cert Manager
    1. Install v1.8.0
    2. Install CRDs with kubectl
    3. Follow https://cert-manager.io/docs/installation/helm/#steps
    
    > Do not follow steps in digital ocean tutorial

  - ### Install cluster issuer
   - Install using `culster-issuer-sample.yaml`

## Commands
DEPLOYMENT_NAME
 - Staging: `livekit-server-staging`
 - Production: `livekit-server-prod`



### Install Helm chart

```
helm install -f ./livekit-server/values.yaml -f override.yaml DEPLOYMENT_NAME ./livekit-server
```

### Upgrade Helm chart

```
helm upgrade -f ./livekit-server/values.yaml -f ./override.yaml DEPLOYMENT_NAME ./livekit-server
```
