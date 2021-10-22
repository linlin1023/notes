
# SSL TLS certificate

a SSL/TLS certificate is a digital certificate than authentictes a website's identity and enables an encryted connection.

SSL = Secure Sockets Layer, which is a security protocol that creates an encrypted link between a web server and a web browser


1. secure online transactions 
2. keep customer information private and secure

TLS (transport layer security) 
it uses encryption algorithms to scramble data in transit to protect sensitive info like :name, address, credit card number, financial details

# work like this
1. browser or server attempts to connect a website secured with SSL
2. the browser or server requests that the web server identifies it self
3. The website sends the browser or server a copy of its SSL certificate in response
4. The browser or server checks to see whether it trusts the SSL certificate, if it does, it signals this to the website

# KALL 6577595----- me to do -----

Vlink to support validation of self signed certificates
* vlink 2.0 support these thing, 
  * which parts need to support
* what is self signed certification
* 

# KALL 6238351

IP needs Kiwiplan software adhere to this new policy
1. Enable TLS 1.2 or greater
2. TLS 1.2 is the only perimtted encryption protocol for SSL or HTTPS connection
3. TLS 1.2 mandatory for all login sessions or any session that transmits sensitive, Restricted or Highly Restricted data
4. IP developed apps, such as those for iPhone or Android, must always use TLS 1.2 and encrypt 100% of traffic.
5. Review the list Permitted Cyphers and implement accordingly
6. The minimum key length must be 2048.
7. Cookies must be explicitly marked as secure when they are created.
8. Enable HTTP Strict Transport Security
9. Certificates must not be expired
10. Certificates must be able to be validated
11. Deploy all required certificates to maintain chain of trust
12. SSL/TLS software must be maintained at current release versions
13. Implement a sustain process to insure patching occurs and that deprecated configurations are removed within 90 days of release.
14. Critical Security Patches must be applied within 30 days of release.
---
MAP MES ESP Mobile, KDW

The lastest communication for auditors is for Web based apps and Mobile, Mobile is already encrypted. Regarding xmgen, currently not a requirement.  Only a handful of machines currently have ability to encrypt


IP will use internally generated certificates, for all VUE products, only one certificate is needed.

IP increased web security also metions implementating HSTS, the requirement is for all new sites to include this extra secutiry, and exiting sites where possible, need to add it. I see where that can be enbaled in **Apache** ,

After testing for this, turns out there will be some FFF changes required, along with possible MES changes.

---

advised IP that they should do testing related to issues certificates(sometimes signed certificates can be a challenge
Regarding HSTS) will be redirected.

HTTP to HTTPS is redirected by default, May need to configure URL,Recommend moving after all else is confiemd to be working

Suggest use preload mechanism which Chrome provided and incorporated by Firefox, Edge, Safari and Opera

https://https.cio.gov/hsts/

https://hstspreload.org/


# KALL 6276421

Running configure.sh is over writing the tomcat server configuration

The information being lost is the following:

Locate the <INSTALLATION_BASE_DIR>/web/<SITE_NAME>/current/conf/server.xml 

file and open it in a text editor.
```XML
Under the <Service> element notice that there are two <Connector> elements which are commented out. One that uses protocol="org.apache.coyote.http11.Http11NioProtocol" and the other that uses protocol="org.apache.coyote.http11.Http11AprProtocol". Uncomment the former (the Connector which Http11NioProtocol) and replace with following:
```

```XML
<Connector port="8443" protocol="org.apache.coyote.http11.Http11NioProtocol"
maxThreads="150" SSLEnabled="true" scheme="https" secure="true">
<SSLHostConfig protocols="TLSv1.2">
<Certificate certificateKeyFile="conf/CertificatePrivateKey.pem"
certificateFile="conf/Certificate.pem"
type="RSA" />
</SSLHostConfig>
</Connector>

```

# KALL 6276432 

Running mesxxx.sh is over writing the tomcat server configuration

When doing the IP security testing we found that whenever mesxxx.sh is run the tomcat server.xml file (tomcat/conf) is over written and the settings for enabling HTTPS for Kiwiplan Web Applications is being lost.

For example, if you re-run the mes installer to install a new product on top of an existing installation. In our case we had QMS and CWR installed in our test environment and when we added OEE into this environment the server.xml was over written. However in addition to this the new file that we also need to create to redirect HTTP traffic to HTTPS is also deleted - the SiteWebDir/current/conf/Catalina/localhost/rewrite.config file.

# KALL 6275822

QMS tab fails in FFF failed to load when using https
Naymesh Mistry
We also tested Bags (with https enabled) which is also an embedded web application within FFF. Bags worked fine i.e. there was no issue with http redirect to https.

Based on this, there are two main areas that need to be looked at.

1) Is Bags using a different embedded browser component/API which handles redirects correctly? If yes, we should use the same for QMS. Or handle http 301 redirect as a valid response and honor it for QMS tab, instead of erroring as seen in the screenshot.

2) For Bags, full URL is configurable in FFF.ini (TARGET property under CUSTOMACTION1 section). Whereas for QMS, only host name (REMOTEHOST property under QMS section) is configurable. The scheme (http) appears to be hard coded in the VB code (clsQMS.vb). We should make this fully configurable like Bags and remove hard coding.

Nick Langstone
25 Jul 2019 10:17
New INI file parameter under QMS
[QMS]
PROTOCOL="https://"

this defines the protocol to communicate with with the QMS server options are...
Also need the remote port number set to the TLS port on the QMS server.

PROTOCOL="https://"
PROTOCOL="http://"

[QMS]
AVAILABLE=True
FAILEDTESTSINMDCGRAPH=False
CANDISABLEFEEDBACK=False
TIMERINTERVAL=60000
REMOTEPORT=8443
REMOTEHOST="xxxxxxx"
HOSTLINETERMINATION=0
POPUPMESSAGE=2
PROTOCOL="https://"

# KALL 6251453

similar to the first KALL IP security policy rolling out

# KALL 6276443

Security certification message is displayed when run configure->secutiry

When doing the IP security testing we found that when we try to access the Configure -> Security option from the QMS swing client a Security Alert message is displayed. 


If the user says Yes to this then the Admin web is opened in HTA and they can proceed.

However this message is re-displayed every time the user tries to access the Configure -> Security menu option.

# KALL 6346571

mshta in URL's even after Web Launcher installed.

We noticed that even after installing the Web Launcher that there are still addresses in summary.log.txt with "mshta".  


suggested checking with development as we were not expecting to see that any longer -- is there a reason or 
can/should it be removed?

Hi Doris,

What revision was this on? We have removed MSHTA urls from 9.20.6 onwards.

# SCM 284643 Naymesh Mistry

HTTPS TLS Support For Kiwiplan Web Applications and REST ...

* MES (java)
* Web Launcher
* 

# SCM 286025


# Code on GIT




# https TLS support document
https://nzgit.kiwiplan.co.nz/kiwiplan/architect-docs/wikis/security/https-tls-support


https://nzgit.kiwiplan.co.nz/naymesh.mistry/docs/-/blob/master/https/HTTPS-TLS-SSL-Investigation.md


https://nzgit.kiwiplan.co.nz/naymesh.mistry/docs/blob/master/https/Enabling%20HTTPS%20for%20Kiwiplan%20Web%20Applications.md



---------------------------video recap---------------------
siteConfiguration.yaml screen
application.yaml screen


swagger UI pcs  proper UI : 172.17.0.1:8080/kp-pcs-service/swagger-ui.html
172.17.0.1:8080/kp-pcs-service/swagger-ui.html/#/Machine/getLineupEntriesV3UsingGET (v1, 6:39)
/v3/machines/{machinenumber}/lineup-entries   (get line up for machine)

(v1 9:41 minutes, has sound)

redirect from http to https 


SSL -> Secure Sockets Layer: 

TLS -> Transport Layer Secure


SSL and TLS are cryptographic protocols that authenticate data
transfer between servers, systems, applciations and users, For example, a cryptographic protocol encrypts the data that is exchanged between a web server and a user.


SSL was a first of its kind of cryptographic protocol, TLS on the other hand, was a recent upgraded version of SSL


----------------------------------------Document Reading--------------------------------------------------------------------------
For IP;s undergoing rolling secrity audit process,   they want to improve address secutiry

IP need all the Kiwiplan web products to support SSL and TLS 1.2 for the communication with all of our product
The web apps must explicity disallow SSL v2/v3 and TLS 1.0 

two broadly used approach
1. Apache as a proxy in fornt of tomcat to provude SSL/TLS 1.2 support
2. Enable SSL/TLS 1.2 support in Tomcat


also for the mobile app used SSL/TLS 1.2


criteria: all web app working and using SSL/TLS 1.2 - and have a ducumented process for IP to manage the installation and replacement of certificates as they expore ever 1- 2 years



For tomcate SSL scenario, from looking at the current configuration , this should be almost entirely a testing effort, with the only special config being installing the certs in Tomcat and confiuring tocmcat to redirect non https traffic to https (Using confidential constrint in web.xml and or rewritecond/rewriterule )


IP are going to confirm what type of cert that will be using - was discussion they were using a self generated cert IP to confirm


Chrome / Firefox,    Safari in furture


It should be noted that TLS provides the above guarantees to data during transmission. TLS does not offer any of these security benefits to data that is at rest. Therefore appropriate security controls must be added to protect data while at rest within the application or within data stores.
    • Use TLS, as SSL is no longer considered usable for security
    • All pages must be served over HTTPS. This includes css, scripts, images, AJAX requests, POST data and third party includes. Failure to do so creates a vector for man-in-the-middle attacks.
    • Just protecting authenticated pages with HTTPS, is not enough. Once there is one request in HTTP, man-in-the-middle attacks are possible, with the attackers being able to prevent users from reaching the secured pages.
    • The HTTP Strict Transport Security Header must be used and pre loaded into browsers. This will instruct compatible browsers to only use HTTPS, even if requested to use HTTP.
    • Cookies must be marked as Secure.

https://cheatsheetseries.owasp.org/cheatsheets/HTTP_Strict_Transport_Security_Cheat_Sheet.html
https://hstspreload.org/
https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#Secure_and_HttpOnly_cookies


PKI: public key infrastructure



Basic Requirements
The basic requirements for using TLS are: access to a Public Key Infrastructure (PKI) in order to obtain certificates, access to a directory or an Online Certificate Status Protocol (OCSP) responder in order to check certificate revocation status, and agreement/ability to support a minimum configuration of protocol versions and protocol options for each version.

SSL vs. TLS
The terms, Secure Socket Layer (SSL) and Transport Layer Security (TLS) are often used interchangeably. In fact, SSL v3.1 is equivalent to TLS v1.0. However, different versions of SSL and TLS are supported by modern web browsers and by most modern web frameworks and platforms.
For the purposes of this cheat sheet we will refer to the technology generically as TLS. Recommendations regarding the use of SSL and TLS protocols, as well as browser support for TLS, can be found in the rule below titled Only Support Strong Protocols.https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#Secure_and_HttpOnly_cookies




----------------------------------------Git doc read----------------------------------------
https://nzgit.kiwiplan.co.nz/kiwiplan/architect-docs/-/wikis/security/https-tls-support

Certificate used must be X.509 standard(https://en.wikipedia.org/wiki/X.509)  and use PEM file format which are most commonly used. This is assumed (not validated) by the configuration tool,- any other format are considered unsupported at this stage and may cause unexpected errors if used.

certificate specified is automatically aded to Kiwiplan Trust Store (kiwiplan.truststore file), both for the tomcate server and JINI services, this is required in order for various client/server compoennt's communication patterns within Kiwiplan ecosystem to work correctly

Kiwiplan Web Launcher



Access vis HTTP port remains available but is automatically redirect to the secure access URL





https://kall.kiwiplan.co.nz/scm/softwareChangeViewer.do?id=284643


