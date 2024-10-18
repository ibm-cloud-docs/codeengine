---

copyright:
  years: 2024
lastupdated: "2024-10-18"

keywords: tls certificate, code engine http endpoint

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Provided TLS certificates for {{site.data.keyword.codeengineshort}} projects
{: #tls-certificate}

{{site.data.keyword.codeengineshort}} applications and functions can be public to the internet, or private inside {{site.data.keyword.cloud_notm}}. In both cases, your application or function is served as an HTTPS endpoint under `codeengine.appdomain.cloud`. {{site.data.keyword.codeengineshort}} provides the TLS certificate for the encryption and regularly rotates it.
{: shortdesc}

## About certificates
{: #certificates-about}

A certificate authority (CA) typically signs TLS certificates that are used in the internet. That way, client applications throughout the world (such as browsers) must trust only the certificates authorized. Further, they do not require knowledge about the certificates of the millions of sites that exist in the internet.

Certificate authorities usually have only a few so-called root certificates, sometimes just one per algorithm (RSA or elastic curves). They are often valid for more than 10 or even 20 years. Certificate authorities use the private key of those root certificates to sign their own intermediate certificates. Those intermediate certificates have a short time in which they are valid, and their private keys are used to sign the leaf certificates for users.

User devices install truststores, which contain the root certificates of all the audited and certified certificate authorities. Operating systems usually contain truststores that all installed programs can use. Some browsers such as Google Chrome or Mozilla Firefox come with their own truststores.

## {{site.data.keyword.codeengineshort}} certificates and their certificate authority
{: #ce-certificates-about}

{{site.data.keyword.codeengineshort}} configures one certificate per project by using a wildcard hostname and therefore applies to all applications and functions that are deployed in that project. The certificates are valid for 90 days; {{site.data.keyword.codeengineshort}} automatically renews them at least ten days before their expiration.

### Let's Encrypt as the certificate authority
{: #ce-certificates-lets-encrypt}

{{site.data.keyword.codeengineshort}} uses [Let's Encrypt](https://letsencrypt.org/certificates) as the certificate authority to sign {{site.data.keyword.codeengineshort}} certificates; these certificates use the RSA algorithm. Therefore, the root certificate of the certificate chain is ISRG Root X1. Any truststore that contains this certificate can be used to access {{site.data.keyword.codeengineshort}}. For a list of operation systems and browser versions that trust ISRG Root X1, see https://letsencrypt.org/docs/certificate-compatibility/#platforms-that-trust-isrg-root-x1.

If you use older versions of browsers or operating systems, then download ISRG Root X1 from https://letsencrypt.org/certificates/. Install it in the relevant truststore by following the instructions of your browser or operating system vendor.

If you want to build your own truststore, trust ISRG Root X1, which you can download from https://letsencrypt.org/certificates/.

### Need more control?
{: #ce-certificates-lets-encrypt-more-control}

Let's Encrypt is a public certificate authority that anybody can use to sign certificates of its own domains. Therefore, trusting ISRG Root X1 means to trust all of these domains.

If you need to trust only your own application, then use custom domain mappings, which give you full control over when you issue and renew the certificate of your own domain. You can set up your client application to trust only the leaf certificate for your domain. You need a process for certificate renewals so that you can switch to a new certificate in the domain mapping’s TLS secret and in your client without communication issues. Typically, you first issue the new certificate. Next, you add it to the client’s truststore. After you update the TLS secret in your {{site.data.keyword.codeengineshort}} project to the new certificate and key, you can remove the old certificate from the client’s truststore.
