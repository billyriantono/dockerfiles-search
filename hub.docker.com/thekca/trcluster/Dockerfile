FROM scratch
COPY script/ca-certificates.crt /etc/ssl/certs/
COPY dist/traefik /
COPY traefik.toml /
COPY acme.json /

EXPOSE 80
EXPOSE 8080
EXPOSE 443

CMD ["/traefik", "-c=/traefik.toml"]
