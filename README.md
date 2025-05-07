# Server configuration

The included `nginx-server.conf` file can be used to set up a **BASIC** https server.
Steps below to create the TLS certificate

## Self signed-certificates

Great for testing, NOT for production stuff. can basically be filled will lorem ipsum and still come out good

1. Create a private key

```bash
openssl genrsa -out domain.key 2048

```

To decode the private key:

```bash
openssl rsa -in examplefile.key -noout

```

2. Create the CSR (Certificate Signing Request)

```bash
openssl req -new -key domain.key -out domain.csr
```

To verify CSR

```bash
openssl req -text -in domain.csr -noout -verify
```

3. Create the Self-signed cert

```bash
openssl x509 -signkey domain.key -in domain.csr -req -days 365 -out domain.crt
```

Verify contents of created cert

```bash
openssl x509 -text -in domain.crt -noout
```

4. Copy to cert and private-key to server

```bash
scp ./domain.crt username@serveraddress:/etc/ssl/certs
scp ./domain.key username@serveraddress:/etc/ssl/certs
```

5. navigate to `https://serveraddress` or `https://localhost` if on the server
