FROM amelia/dhparam:latest as dhparam
FROM nginx:alpine

COPY --from=dhparam /etc/ssl/dhparam.pem /etc/nginx/certs/dhparam.pem
COPY --from=dhparam /etc/ssl/snakeoil-cert.pem /etc/nginx/certs/certificate.pem
COPY --from=dhparam /etc/ssl/snakeoil-key.pem /etc/nginx/certs/privkey.pem
RUN rm -fv /etc/nginx/conf.d/default.conf
COPY site.conf /etc/nginx/conf.d/site.conf
