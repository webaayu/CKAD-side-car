
# Steps:

## Create certificate

$ openssl req -x509 -newkey rsa:2048 -keyout tls.key -out tls.crt -nodes -subj '//CN=echo-server'

## Add secrets to the keyvault

$ az keyvault secret set --vault-name cy-key-vault-demo --name "TLS-CERT-CRT" --file tls.crt

$ az keyvault secret set --vault-name cy-key-vault-demo --name "TLS-CERT-KEY" --file tls.key

## Create ConfigMap

$ kubectl create cm nginx-conf --from-file nginx.conf

## Create Secret-Provider-Class to get secrets from Keyvault

$ kubectl apply -f secret-provider-class.yaml

## App Deployment

$ kubectl apply -f deployment.yaml

$ kubectl get pods

$ kubectl get svc

## Run

Go to browser and use <load-balancer-ip> with both http ans https.

