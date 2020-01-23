FROM alpine:3.10
# hadolint ignore=DL3018
RUN apk add --no-cache ca-certificates stunnel gettext tini
COPY --chown=root:root entrypoint /usr/local/sbin/
COPY --chown=root:root stunnel.conf /etc/stunnel/stunnel.conf.tmpl
ENTRYPOINT ["entrypoint"]
CMD ["stunnel"]
ENV DEBUG="5" \
    CLIENT="yes"
