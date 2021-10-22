# What is HSTS
## HSTS is Http Strict Transport Security

When a browser knows that a domain has enabled HSTS, it does two things
1. always uses an htts:// connection, even when clicking on an http:// link, or without specifying a protocol
2. remove the ability for users to click through warning about invalid certificates.

A domain instructs browsers that it has enabled HSTS by returing an HTTP header over an HTTPS connection

simplest form, the policy tells a browser to enable HSTS for that exact domain or subdomain, and to remember it for a given  number of seconds:
Strict-Transport-Security: max-age=31536000;

In its strongest and recommended form, the HSTS policy includes all subdomains, and indicates a willingness to be "preloaded" into browsers:
Strict-Transport-Security: max-age=31536000; includeSubDomain; preload

Whenusing above form, bear in mind:
1. the policy should be deployed at https://domain.gov , not 
https://www.domain.gov
2. All subdomain associated with the parent domain must support HTTPS, they do not have to each have their own HSTS policy

## Backgroud
The basic problem tha HSTS solves is that even after website turns on HTTPS, visitors may still end up trying to connect over plain HTTP, for Example:
1. when a user types "gsa.gov" into the URL bar, browser default to using http://
2. A user may click on an old link that mistakenly uses an http:// URL
3. A user's network may be hostile and actively rewrite https:// links to http://
Websites that prefer HTTPS will generally still listen for connections over HTTP in order to redirect the user to the HTTPS URL. For Example

$ curl --head http://github.com
HTTP/1.1 301 Moved Permanently
Location: https://github.com/

> This redirect is insecure and is an opportunity for an attacker to capture information about the visitor(such as cookies from a previous secure session), or to maliciously redirect the user to a fishing site

this can be addresssed by returing a Strict-Tranport-Security header whenever the user connects securely.

$ curl --head https://github.com
HTTP/1.1 200 OK
Strict-Transport-Security: max-age=31536000; includeSubdomains; preload

This enables HSTS for github.com. while HSTS is in effect, clicking any links to http://github.com will cause the browser to issue a request directly for https://github.com.

In above example, the browser will remeber the HSTS policy for a year, the policy is refreshed every time browser sees the header again, so if a user visits https://github.com at lease once a year, they will be indefinitely protected by HSTS. 


HSTS Preloading
the Chrome secutry team created an "HSTS preload list":  A list of domains baked into Crhome that get Strict Transport Security enabled automatically, even for the first visit.
Firefox, Safati, Opera and Edge also incorporate Chrome;s HSTS preload list, making this feature shared across major browsers

An example of a valid HSTS header for preloading:
Strict-Transport-Security: max-age=31536000; includesSubDomains; preload


In the long term, as the web transitions fully to HTTPS and browsers can start phasing out plain HTTP and defaulting to HTTPS, the HSTS preload list(and HSTS itself) may eventually become unnecessary.

Util that time, the HSTS preload list is a simple effective mechanism for locking down HTTPS for an entire domain.


# Reference
> To resolve the redirect dangerous, to turn on Strict Transport Secutiry and send direct https request when http is used [HSTS](https://https.cio.gov/hsts/)


> To regist into browser that automatically enable Strict Transport Secutiry even for the first time visit the website [Preload](https://hstspreload.org/)




