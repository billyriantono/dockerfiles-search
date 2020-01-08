FROM alpine:latest

LABEL author="me"

COPY palm-springs /palm-springs
RUN chmod +x palm-springs

EXPOSE 8080

ENTRYPOINT ["/palm-springs"]
