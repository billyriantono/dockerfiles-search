FROM nginx:alpine

# Install consul template.
ADD https://releases.hashicorp.com/consul-template/0.14.0/consul-template_0.14.0_linux_amd64.zip /tmp/
RUN unzip /tmp/consul-template_0.14.0_linux_amd64.zip -d /usr/local/bin

# Remove nginx config dir.
RUN rm -rf /etc/nginx/conf.d

# Add SSL certificates
COPY ./nginx.crt /etc/nginx/ssl/nginx.crt
COPY ./nginx.key /etc/nginx/ssl/nginx.key

# Add nginx template.
COPY ./nginx.conf.ctmpl /tmp/nginx.conf.ctmpl

# Add entrypoint script.
COPY ./entrypoint /tmp/entrypoint
RUN chmod 755 /tmp/entrypoint
CMD ["/tmp/entrypoint"]
