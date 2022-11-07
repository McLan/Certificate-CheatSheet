# Certificate CheatSheet
Linux commands working with certificates

## Add certificate to trusted certs (Linux)
1. Copy cert to :
* /usr/local/share/ca-certificates/ (debian) 
* /etc/pki/ca-trust/source/anchors/ (redhat)

2. Run 
```
sudo update-ca-certificate
```

## Sign sub CA certificate with AD CS (save it in .cer)
```
certreq -submit -attrib "CertificateTemplate:SubCA" pki_intermediate.csr
```

## Get certificate with openssl
```
openssl s_client -showcerts -servername www.example.com -connect www.example.com:443 </dev/null
```


# Checking 
## Check certificate
```
openssl x509 -in certificate.crt -text -noout
```

## Check private key 
```
openssl rsa -in key.pem -check
```

## Check CSR 
```
openssl req -text -noout -verify -in req.csr
```

## Check PKCS file (.p12 or .pfx)
```
openssl pkcs12 -info -in keyStore.p12
```

# Converting
## DER (.cer, .der and .crt) to PEM
```
openssl x509 -inform der -in certificate.cer -out certificate.pem
```

## PEM to DER
```
openssl x509 -outform der -in certificate.pem -out certificate.der
```

## PKCS 12 (.pfx and .p12) to PEM
```
openssl pkcs12 -in keyStore.pfx -out keyStore.pem -nodes
```

## PEM to PKCS 12 
```
openssl pkcs12 -export -out certificate.pfx -inkey privateKey.key -in certificate.crt -certfile CACert.crt
```


# Certificate generation
## Generate private key and csr
```
openssl req -out CSR.csr -new -newkey rsa:2048 -nodes -keyout privateKey.key
```

## Generate self-signed certificate
```
openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout privateKey.key -out certificate.crt
```

## Generate a certificate signing request (CSR) for an existing private key 
```
openssl req -out CSR.csr -key privateKey.key -new
```

## Generate a certificate signing request based on an existing certificate 
```
openssl x509 -x509toreq -in certificate.crt -out CSR.csr -signkey privateKey.key
```

## Remove a passphrase from a private key 
```
openssl rsa -in privateKey.pem -out newPrivateKey.pem
```