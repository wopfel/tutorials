Transitioning from blacklabelops/letsencrypt to certbot/certbot docker
======================================================================

In the past, I've renewed my Let's Encrypt certificates for Nginx by using the docker container provided by blacklabelops. This has been working for several months. I was using the built-in webserver (meaning I was stopping Nginx prior updating the certificate).

Some days in March 2019 I've got a mail from Let's Encrypt:

```
Action may be required to prevent your Let's Encrypt certificate renewals from
breaking.

If you already received a similar e-mail, this one contains updated information.

Your Let's Encrypt client used ACME TLS-SNI-01 domain validation to issue a
certificate in the past 12 days. Below is a list of names and IP addresses
validated (max of one per account):

TLS-SNI-01 validation is reaching end-of-life. It will stop working
permanently on March 13th, 2019. Any certificates issued before then will
continue to work for 90 days after their issuance date.

You need to update your ACME client to use an alternative validation method
(HTTP-01, DNS-01 or TLS-ALPN-01) before this date or your certificate renewals
will break and existing certificates will start to expire.
```

I've searched for an updated docker container, but the docker stuff has been migrated to blacklabelops-legacy. The container won't get any updates in the future.

Using certbot/certbot
---------------------

This was a perfect opportunity to switch to the webroot challenge, so I don't have to stop my docker-compose (with Nginx inside) any longer.

Configuration file for the Nginx proxy server (excerpt):

```
server {
    listen 80;
    listen [::]:80;
    server_name my-domain.example.com;
    location ^~ /.well-known {
        allow all;
        default_type text/plain;
        root /var/www/html-letsencrypt;
    }
    location / {
        return 301 https://$server_name$request_uri;
    }
}
```

Docker compose file (excerpt):
```
services:
  proxy:
    image: nginx:alpine
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx-proxy.conf:/etc/nginx/conf.d/default.conf:ro
      - ./letsencrypt:/etc/nginx/certs:ro
      - ./letsencrypt-acme:/var/www/html-letsencrypt:ro
```

Renewing the certs:

```
cd /directory/with/docker-compose-file/
docker run --rm -it --name certbot -v ./letsencrypt:/etc/letsencrypt -v ./letsencrypt-acme:/var/www/acme-challenge certbot/certbot certonly --webroot -w /var/www/acme-challenge/ -d my-domain.example.com --renew-by-default --email my-mail-address --agree-tos
```

Reloading Nginx proxy:

```
docker-compose exec proxy sh
nginx -s reload
exit
```

Or, alternatively, reloading in one command:

```
docker-compose exec proxy sh -c "nginx -s reload"
```

