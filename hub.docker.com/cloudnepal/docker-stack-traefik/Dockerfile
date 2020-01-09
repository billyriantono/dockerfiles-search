FROM traefik:v2.1.1

# put traefik config
RUN mkdir -p /etc/traefik/
COPY ./traefik.toml /etc/traefik/traefik.toml

EXPOSE 80
EXPOSE 443
