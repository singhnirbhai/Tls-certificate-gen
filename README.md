# Tls-certificate-gen

## Create directory 
```bash
mkdir certs
```

## Generate the private key for your CA-signed certificate
```bash
openssl genrsa -out training.key 4096
```

## Generate the certificate signing request (CSR) for the todo-https.apps.ocp4.example.com hostnam
```bash
openssl req -new \
-key training.key -out training.csr \
-subj "/C=US/ST=North Carolina/L=Raleigh/O=Red Hat/\
CN=todo-https.apps.ocp4.example.com"
```
Finally, generate the signed certificate. Notice the use of the -CA and -CAkeyoptions for signing the certificate against the CA. Use the -passin option to reuse the password of the CA. Use the extfile option to define a Subject Alternative
Name (SAN).
```bash
openssl x509 -req -in training.csr \
-passin file:passphrase.txt \
-CA training-CA.pem -CAkey training-CA.key -CAcreateserial \
-out training.crt -days 1825 -sha256 -extfile training.ext
```
## Check the certificate
```bash
ls -lrt
