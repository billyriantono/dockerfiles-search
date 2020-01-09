FROM haproxy:1.9

## 14 June 2019 - Commented out packages are not available until debian buster - which is in testing. This container runs stretch.
RUN apt-get update \ 
  && apt-get install -y certbot python3-certbot-dns-cloudflare \ 
  python3-certbot-dns-route53 \
  python3-certbot-dns-digitalocean \
  python3-certbot-dns-linode \
  python3-certbot-dns-google

