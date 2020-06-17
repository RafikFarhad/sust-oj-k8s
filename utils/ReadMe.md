# Cert Managment

### Create a certificate authority

    openssl genrsa 2048 > ca-key.pem
    
    openssl req -new -x509 -nodes -days 365 -key ca-key.pem > ca-cert.pem


### Create a certificate for the server using the CA certificate generated above

- __The Common Name used here must differ from the one used for the Certificate Authority above.__

```
openssl req -newkey rsa:2048 -days 365 -nodes -subj "/C=BD/ST=Dhaka/L=Dhaka/O=SUST/OU=OJ/CN=mysql-service.sourcecode" -keyout server-key.pem > server-req.pem

openssl x509 -req -in server-req.pem -days 365 -CA ca-cert.pem -CAkey ca-key.pem -set_serial 01 > server-cert.pem
```

### Create a certificate for the clients using the same CA certificate

- __Provide the details for the client that will connect to the server.__

- __The Common Name used here must differ from the one used for the Certificate Authority and the Server certificate above.__

```
openssl req -newkey rsa:2048 -days 365 -nodes -subj "/C=BD/ST=Dhaka/L=Dhaka/O=SUST/OU=OJ/CN=$USER" -keyout client-key.pem > client-req.pem 

openssl x509 -req -in client-req.pem -days 365 -CA ca-cert.pem -CAkey ca-key.pem -set_serial 01 > client-cert.pem
```


## [FreeCodeCamp OpenSSL Sheet](https://www.freecodecamp.org/news/openssl-command-cheatsheet-b441be1e8c4a/)