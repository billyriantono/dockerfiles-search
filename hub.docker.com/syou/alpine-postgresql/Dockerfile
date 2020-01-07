FROM alpine:3.5

ENV PGHOME=/var/lib/postgresql \
    PGDATA=/var/lib/postgresql/data

RUN apk add --no-cache postgresql \
	&& mkdir -p ${PGHOME} ${PGDATA} \
	&& chown -R postgres ${PGHOME} \
	&& rm -rf /var/cache/apk/*

VOLUME /var/lib/postgresql

EXPOSE 5432

USER postgres

CMD [ "postgres" ]

