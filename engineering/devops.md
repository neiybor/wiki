<!-- TITLE: DevOps -->
<!-- SUBTITLE: DevOps info -->

# DevOps
## Managing SSL certificates

### Requesting a certificate
```
openssl req -new -newkey rsa:2048 -nodes -keyout star.neiybor.com.key -out star.neiybor.com.csr
```

Fill in prompts as follows
```
Generating a 2048 bit RSA private key
...
writing new private key to 'star.neiybor.com.key'
...
Country Name (2 letter code) [AU]:US
State or Province Name (full name) [Some-State]:Utah
Locality Name (eg, city) []:Lehi
Organization Name (eg, company) [Internet Widgits Pty Ltd]:Neighbor Storage, Inc.
Organizational Unit Name (eg, section) []:
Common Name (e.g. server FQDN or YOUR name) []:*.neiybor.com
Email Address []:ops@neighbor.com

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:
An optional company name []:

```

### Downloading
Download from web page and not the zip file that gets emailed. ssls.com does not include the p7b file in the emailed zip file.

### Creating PEM file
Some services require the certificate to be uploaded in a .pem format.
```
openssl pkcs7 -print_certs -in star.neiybor.com.p7b -out star.neiybor.com.pem
```

### Uploading to Amazon
In Amazon Certificate Manager (ACM) upload the certificate as follows.
1. In the `Certificate body` input paste the contents of the .crt file.
2. In the `Certificate private key` input paste the contents of the .key file.
3. In the `Certificate chain` input paste the contents of the .ca-bundle file.

## Certificate uses
When changing the Neighbor.com certificate here are places that will need to be updated:
* cloudfront distro for intercom
* cloudfront distro for naked domain
* cloudfront distro for www.neighbor.com
* heroku frontend server
* blog server
* cms / drupal server
* heroku wiki server