# Generate SSL certificates and DNS records


1.  Install an SSL key generation tool. In this tutorial we use
    [OpenSSL](https://www.openssl.org/) as the tool.

2.  On the command-line, navigate to a preferred location in the server
    and execute the following command to generate a private SSL key with
    the name `private.key`.

    ``` java
    openssl genrsa -out private.key 2048
    ```

    Note that the key file is generated in the directory location that
    you are in.

3.  In the command-line, execute the following command to generate a
    certificate signing request file for your custom URL. Be sure to
    change the business address in this command to your own.

    ``` java
    openssl req -new -key private.key -sha256 -nodes -out request.csr -subj "/C=US/ST=California/L=Mountain View/O=WSO2/OU=IT/CN=developers.mytesturl.info"
    ```

    !!! tip
    
        The certificate signing request file is generated in the directory location that you are in.<br/> You can go to a certificate vendor of your choice and use the certificate signing request file to obtain a certificate for your domain. Any certificate that is accepted by browsers work. Here we have used <https://www.comodo.com/> as the certificate authority.  
      
    When you are done, you typically receive an email with the
    certificate for your domain along with the certificate authority's
    root and intermediate certificates. Some certificate authorities
    provide the root and intermediate files as a single chain file, some
    others provide multiple files, and some others provide none.

    !!! tip
    
        When receiving certificate files (private key and public
        key) from vendors, they may provide certificates of different file
        types (E.g., `.crt`, `.cer`, `.p7b`, `.pem`, `.pfx`).
        However, when uploading the public certificate in WSO2 API Cloud,
        the preferred formats are `.crt`,`.cer`,and `.pem`. Therefore,
        if you have a public certificate file of any other type(
        `.p7b`,`.pfx`), you need to convert them to the
        preferred file type.
    
        You can use the **OpenSSL** command to convert the certificate files
        as shown in the examples below:
      
    
        ``` java
        Convert P7B to PEM: openssl pkcs7 -print_certs -in certificatename.p7b -out certificatename.pem
        Convert PFX to PEM: openssl pkcs12 -in certificate.pfx -out certificate.pem -nodes
        ```


4.  If you receive multiple root and intermediate files from your
    certificate authority, use the `           cat          ` utility
    (available in Unix and Unix-based operating systems) to concatenate
    them into a single chain file ( `           chain.crt          ` ).
    An example is given below.

    ``` java
    cat COMODORSADomainValidationSecureServerCA.crt COMODORSAAddTrustCA.crt AddTrustExternalCARoot.crt > chain.crt
    ```

    If you are using **Microsoft** **Windows,** follow the
    instructions below to concatenate the files.

    -   Open all certificate files except your domain certificate in a
        text editor.

    -   Create a new blank text file.

    -   Copy the contents from all the files in the reverse order and
        paste them into the new text file. For example, copy
        intermediate 3, intermediate 2, intermediate 1, and then the
        root certificate.

    -   Save the newly created file (say chain.crt).

    **The `chain.crt` file should have content in the following
    order:**

    ``` java
    -----BEGIN CERTIFICATE-----
    (Your Intermediate certificate: COMODORSADomainValidationSecureServerCA.crt)
    -----END CERTIFICATE----- 
    
    -----BEGIN CERTIFICATE-----
    (Your Intermediate certificate: COMODORSAAddTrustCA.crt)
    -----END CERTIFICATE-----
    
    -----BEGIN CERTIFICATE-----
    (Your Root certificate: AddTrustExternalCARoot.crt)
    -----END CERTIFICATE-----
    ```

5.  Reserve a domain name with any domain registrar and create DNS CNAME
    records that map the domain to your API Store and Gateway URLs.

    !!! note

        Most domain registrars provide step-by-step instructions in their websites. For your convenience, we have listed the general steps below.

        Expand to see the listed steps

         -   Sign in to the domain registrar’s site.
         -   Navigate to your Domain Name Server (DNS) management page. The
        location and name of this page can vary by the host, but can
        generally be found under the **Domain Managemen** t or
        **Advanced Settings** section.
         -   Find the CNAME settings. Under the 'CNAME value or alias', enter
        the subdomain that you want to map each URL to. The subdomain of
        [developers.mytesturl.info](http://developers.mytesturl.info/)
        is developers.
         -   Set the CNAME destination to the API Cloud's custom DNS
        endpoint, which is
        [customdns.api.cloud.wso2.com](http://customdns.api.cloud.wso2.com/)
        . When configuring a custom URL for API gateway, if you select a
        region different from the default region (US East), be sure to
        set the CNAME destination according to the following table.

          | Region         | Pointing URL                     |
          |----------------|----------------------------------|
          | US East        | customdns.api.cloud.wso2.com     |
          | US West        | customdns-usw.api.cloud.wso2.com |
          | Sydney         | customdns-syd.api.cloud.wso2.com |
          | Brazil         | customdns-brz.api.cloud.wso2.com |
          | EU (Ireland)   | customdns-ire.api.cloud.wso2.com |
          | EU (Frankfurt) | customdns-frk.api.cloud.wso2.com |


<html>
         <div class="admonition info">
         <p class="admonition-title">Note</p>
         <p>WSO2 API Cloud allows the use of self-signed certificates for
        educational purposes and internal usage, but we **do not recommend**
        the use of self-signed certificates in production environments.</p>
         </div>
</html>      
    

Now you have the required SSL certificates and DNS records to configure custom URLs for API Cloud.
You can take a look at the following topics for instructions on how to customize
the API Store, Publisher, Admin portal, and Gateway domains.
