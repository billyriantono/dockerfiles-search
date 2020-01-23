FROM davask/d-base:d8.8
MAINTAINER davask <docker@davaskweblimited.com>
USER root
LABEL dwl.server.http="node 6-d8.8"

RUN curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
# Update packages
RUN apt-get update && \
apt-get install -y nodejs
RUN apt-get upgrade -y && \
apt-get autoremove -y && \
apt-get clean && \
rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# install angular-cli
RUN npm install -g @angular/cli

# Configure Node
# 80 = HTTP, 443 = HTTPS, 35729 = livereload, 8080 = node-inspector
EXPOSE 80 443 35729 8080

HEALTHCHECK --interval=5m --timeout=3s \
CMD curl -f http://localhost/ || exit 1

COPY ./build/dwl/init.sh \
./build/dwl/ng.sh \
/dwl/

CMD ["/bin/bash /dwl/init.sh"]

RUN chmod +x /dwl/init.sh && chown root:sudo -R /dwl
USER admin
