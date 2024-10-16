$ openssl req -x509 -newkey rsa:2048 -keyout tls.key -out tls.crt -nodes -subj '//CN=echo-server'

az keyvault secret set --vault-name cy-key-vault-demo --name "TLS-CERT-CRT" --file tls.crt

az keyvault secret set --vault-name cy-key-vault-demo --name "TLS-CERT-KEY" --file tls.key

kubectl create cm nginx-conf --from-file nginx.conf
