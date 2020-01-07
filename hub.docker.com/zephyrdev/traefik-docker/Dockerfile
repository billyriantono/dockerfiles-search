FROM traefik

COPY templates/eureka.tmpl /templates/
COPY traefik.toml /etc/traefik/
COPY cert /etc/traefik/cert

ENTRYPOINT ["/traefik"]

