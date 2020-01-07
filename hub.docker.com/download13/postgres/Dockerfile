FROM download13/alpine-tls

WORKDIR /data
RUN apk-install postgresql && \
	chown postgres:postgres /data
USER postgres
RUN initdb -D /data
COPY pg_hba.conf pg_hba.conf

CMD ["postgres", "-D", "/data", "-c", "listen_addresses=*"]
