# Get tfnotify
FROM alpine:3.7 AS tfnotify

ARG VERSION=0.1.0

RUN wget -O - https://github.com/mercari/tfnotify/releases/download/v${VERSION}/tfnotify_v${VERSION}_linux_amd64.tar.gz | tar zxvf - -C /tmp \
 && install -m 0755 /tmp/tfnotify_v${VERSION}_linux_amd64/tfnotify /tmp


# Install tfnotify to hashicorp:terraform:light
FROM hashicorp/terraform:light

COPY usr/local/bin/entrypoint.sh /usr/local/bin/entrypoint.sh
COPY --from=tfnotify /tmp/tfnotify /usr/local/bin/tfnotify

RUN chmod +x /usr/local/bin/tfnotify /usr/local/bin/entrypoint.sh

ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
