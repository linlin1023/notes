# openssl

# keytool

> keytool is a key and certificate management utility, it allows uses to administer their own public/private key pairs and associated certificates for use in self-authentication (where user authenticates himself/herself to other users/services) or data integrity and authentication services, using diital signatures. It allows uses to cache the public keys (in the form of certificates)


~~~shell
$ keytool -importkeystore -destkeystore vlink2key.jks -srckeystore vlink2key.p12  -srcstoretype pkcs12 -alias servercert
~~~
