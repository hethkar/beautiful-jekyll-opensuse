---
layout: post
title: 'How to install Let's Encrypt SSL for your websites in Cpanel'
---
# How to install Let's Encrypt SSL for your websites in Cpanel

Go to the Security Sectiom of your Cpanel 
You will find a SSL/TLS option under Security.
In the SSL/TLS page you will have the following sections.
 
### Private Keys (KEY)
Generate, view, upload, or delete your private keys.

### Certificate Signing Requests (CSR)
Generate, view, or delete SSL certificate signing requests.

### Certificates (CRT)
Generate, view, upload, or delete SSL certificates.

### Install and Manage SSL for your site (HTTPS)
Manage SSL sites.


First you will need generate a private key and CSR 
Click the `Generate, view, or delete SSL certificate signing requests.` under CSR section.

The first field is the `Key` with a drop down menu.
You can generate your private key here
Option- Generate a new 2,048 bit key. (or if you have generated any private keys before it will be displayed in the drop down menu)

Next field is the Domains text box.
Here you will have to give your domain name for which you will be getting your SSL certificate from Let's Encrypt.
When it comes to Let's Encrypt if you want to have your SSL certificate for www.example.com , then you will have to mention www.example.com (with www included) in the 
Domains text box, else if you don't want the www then you can just add your domain name as example.com .

Fill the rest of the fields.

Your CSR will be generated once you fill all mandatory fields and click on Generate button.

Copy of you CSR. 

Go to https://zerossl.com/ 

Click on Online Tools

Go to FREE SSL Certificate Wizard
(Free SSL certificates trusted by all major browsers issued in minutes.)

Start the wizard.

You can give your email in the email field. This will be helpful as you will receive notifications about the certificate expiration date, though it is optional.
Paste the generated CSR in the right column.
Check the HTTP verification Check box.
Check the Accept ZeroSSL TOS , Accept Let's Encrypt SA (pdf) Check boxes.

On the left column a Let's Ecnrypt Key will be generated ( which you can copy and keep it with you as it will be needed when we want to renew the certificate )

Click on Next 
Here you will get
The name for the file you will have to create .
location where you have to create. (public_html/.well-known/acme-challenge/filehere)
contents that file should have.

Once you have create you can open the link in a new tab and check if you're able to view the contents of the file from the website.

In the third step you will get you certificate generated. 

You can copy your certicate and download it as well. 





Installing the Certificate in the cPanel.

In the cPanel click on `Manage SSL sites.` under Install and Manage SSL for your site (HTTPS) .
Select your domain under the domain drop-down menu.
Paste your certificate under - Certificate: (CRT)
Once you paste your CRT, an autofill button will show up on the side - which will fill the rest of the sections.
Then click on the Install Certificate button which will the install the certificate.

It will take sometime for the Certificate to reflect on the website.





