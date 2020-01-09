FROM alpine

LABEL maintainer="sven.szejwach@squarescale.com"

ADD https://gist.github.com/ika108/5a9311e6b2f58672518d1bf6ccade68c/raw/a5e27fa9dfc46a92d9a3d1aca504894b68e5a76a/sqsc-cli /bin/sqsc-cli

COPY docker-entrypoint.sh /

RUN chmod +x /bin/sqsc-cli /docker-entrypoint.sh

RUN apk add ca-certificates

ENTRYPOINT ["/docker-entrypoint.sh"]

CMD ["deploy"]
