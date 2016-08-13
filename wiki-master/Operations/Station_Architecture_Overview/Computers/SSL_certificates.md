*Current status:* Certificates are OK until 7PM 11/26/17. Reissued 4/9/14.

Servers that have this cert:

-   wmfo-linode.wmfo.org
-   wmfo-duke.orgs.tufts.edu
-   wiki.wmfo.org

 

We buy wildcard certificates for \*.wmfo.org that cover both the public website, hosted by Dreamhost, and this wiki, hosted on a VM on Smoothcriminal. When updating the certificates, it is necessary to update them in both places.

1.  Backup the old key/cert pair.
2.  If the key is compromised, you'll need to create a new Key and CSR (Certificate Request something something) to send to the SSL Cert Authority. To create a new key (on Duke the folder is currently /opt/wmfo/certs), you'll want to type \`openssl genrsa -out wmfo.org.key 2048\` assuming you need a 2048 bit modulus. This is probably good practice anyways every time you renew the certificate.
3.  To create the CSR, type \`openssl req -new -key wmfo.org.key -out wmfo.org.csr\`. It will ask you for information. See bottom of page.
4.  If this is a new certificate, you'll need to pay. If this is a "reissue," you can simply enter visit the page on SSLs.com (they changed their domain ;) and press Reissue.
5.  Open up the CSR you just generated (\`less wmfo.org.csr\`) and copy and paste it into the Request box. Select appropriate confirmation email. Confirm the email they send you. Enter information on SSLs.com. Cert will be emailed to you.
6.  Set up the new certificate. This can be done by simply replacing the old one and restarting Apache or by making a new one and editing every instance of the /etc/apache2/sites-available/site.ssl file to reference the new file. You will also need the root certificate for SSLs.com (/Comodo or whichever CA they shunt you to) for some browsers to be "happy." See bottom of page.
7.  Open wmfo.org in a browser and inspect the certificate. Ensure that the new certificate is running (check the expiration date).

 

For the Wiki:

1.  On Smooth, take a snapshot of the wiki.
2.  ssh into wiki.wmfo.org and move the old files in \~/ssl to \~/ssl/old, which you should clear out first.
3.  From your ssl directory on Duke or wherever, run `scp cert-files user@wiki.wmfo.org:~/ssl`, where cert-files are all the new certificate files (if you have a .zip, use that) and user is the actual username. Enter the password when prompted. If you used a .zip, unzip it. You'll need to su to root to do these because no sudo is setup.
4.  Now that you have the files on disk, it is time to put them in the apache server. Still ssh'd into wiki.wmfo.org, move the old files in /etc/apache2/ssl to /etc/apache2/ssl/old, which you should clear out first. This is at the top level, above the home folder where you were before.
5.  Run `cd ~/ssl;cp cert-files /etc/apache2/ssl`, again replacing cert-files with the real files. Again, you can move the .zip and then go unzip it.
6.  Apache looks for the certificates in the paths given in /etc/apache2/sites-enabled/dekiwiki but those paths should remain the same. Unless the file names are different, in which case update the file.
7.  Open wiki.wmfo.org in a browser and inspect the certificate. Ensure that the new certificate is running (check the expiration date).
8.  Once you know everything is working for a day or so, make another known-good snapshot of the vm. This will erase the previous snapshot, so be good and certain.
9.  Backup everything to super using the synctoy job (wiki may need to be shutdown to do this without a file in use error).

 

Nick's SSL Info:

Country Name (2 letter code) [AU]:US

State or Province Name (full name) [Some-State]:Massachusetts

Locality Name (eg, city) []:Medford

Organization Name (eg, company) [Internet Widgits Pty Ltd]:WMFO, Tufts Freeform Radio

Organizational Unit Name (eg, section) []:Operations Department

Common Name (e.g. server FQDN or YOUR name) []:\*.wmfo.org

Email Address []:[ops@wmfo.org](mailto:ops@wmfo.org "mailto:ops@wmfo.org")

 

Typical SSL config in an Apache 2 + openSSL setup virtualhost:

        SSLCertificateFile /opt/wmfo/certs/server.crt

        SSLCertificateKeyFile /opt/wmfo/certs/server.key

        SSLCertificateChainFile /opt/wmfo/certs/wmfo.ca-bundle

 

 

Some threads on this: [wmfo-ops] thread called "Re: [wmfo-ops] Certificates" dated 3/14/12 and "[wmfo-ops] wiki permissions struggles" dated 11/27/12. (But ignore them, this page is correct. --Nick)

*
