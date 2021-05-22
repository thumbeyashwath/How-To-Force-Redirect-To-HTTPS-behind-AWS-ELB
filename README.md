# How-To-Force-Redirect-To-HTTPS-behind-AWS-ELB


Reference: https://tecadmin.net/force-redirect-https-behind-aws-elb/

Your web server is running on port 80 to listen http connections on AWS Ec2 instnace. After that configured AWS ELB to listen on HTTP and HTTPS protocols and forwarding all the requests to backend server on port 80 only. The Amazon Elastic Load Balancer (ELB) supports X-Forwarded-Proto header value include the protocol of application.

This tutorial uses X-Forwarded-Proto header value of the HTTP request, and apply the rewrite rules if the client protocol is not HTTPS. Here is the configuration details for Apache, Nginx and IIS to force redirect to HTTPS behind AWS ELB .
--------------------------------------------------------------
1. Apache
Edit Apache VirtualHost configuration file in text editor and add the following content. Make sure rewrite module is enabled in Apache server.
````
<VirtualHost *:80>
  
  RewriteEngine On
  RewriteCond %{HTTP:X-Forwarded-Proto} !https
  RewriteRule ^.*$ https://%{SERVER_NAME}%{REQUEST_URI}
</VirtualHost>
````
--------------------------------------------------------------
2. NGINX

Edit Nginx HTTP server block for your domain to configure force redirection. Add the following content under location block to redirect all http traffic to https.
````
server {
 listen 80;
 ...
 location / {
  if ($http_x_forwarded_proto != 'https') {
  rewrite ^ https://$host$request_uri? permanent;
  }
 }
}
````
--------------------------------------------------------------
3. IIS
The windows servers with IIS web server edit the web.config file and add the following code under the section:
````
<rewrite>
<rules>
<rule name="AWS ELB Forece Redirect to HTTPS" stopProcessing="true">
<match url="^(.*)$" ignoreCase="false" />
<conditions>
<add input="{HTTP_X_FORWARDED_PROTO}" pattern="^http$" ignoreCase="false" />
</conditions>
<action type="Redirect" redirectType="Found" url="https://{HTTP_HOST}{REQUEST_URI}" />
</rule>
</rules>
</rewrite>
````
