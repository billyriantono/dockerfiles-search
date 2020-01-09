FROM alpine:3.9

# add user unbound as system user and create homedir
RUN adduser -S -h /home/unbound unbound; addgroup -S unbound;
# set env var
ENV PATH $PATH:/usr/local/lib

# Install package
RUN apk --no-cache add unbound openssl

# add configutation
COPY files/unbound.conf /usr/local/etc/unbound/unbound.conf
# prepare runtime
RUN mkdir /usr/local/etc/unbound/conf.d
RUN chown -R unbound:unbound /usr/local/etc/unbound/ /etc/unbound

# Entrypoint script
COPY files/entrypoint.sh /entrypoint.sh

# Switch to unbound user
USER unbound
# download files from root '.' server
RUN unbound-anchor -a /usr/local/etc/unbound/root.key ; true
RUN wget https://www.internic.net/domain/named.root -O /usr/local/etc/unbound/root.hints

USER root
# expose the ports
EXPOSE 53/udp
EXPOSE 53

WORKDIR /usr/local/etc/unbound

# start script
CMD ["/entrypoint.sh"]
