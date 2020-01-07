FROM opsbears/base:stable

RUN apt-get install -y nginx-extras lua-nginx-dns lua-nginx-string && mkdir -p /etc/nginx/ssl
COPY etc /etc
COPY init.sh /init.sh
RUN cat /etc/nginx/nginx.conf | perl -pe 's/http \{/http \{\n\tinclude resolvers.conf;/' >/tmp/nginx.conf && mv /tmp/nginx.conf /etc/nginx/nginx.conf && rm /etc/nginx/sites-enabled/default

# Allow long startup period so the dhparam generation can finish. You may want to override this.
HEALTHCHECK --interval=5s --timeout=5s --start-period=120s CMD curl --fail http://localhost:80/ || exit 1

CMD ["/init.sh"]
