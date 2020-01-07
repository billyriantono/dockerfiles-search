FROM ubuntu:18.04

RUN apt update && apt install -y supervisor postgresql curl nginx

# Install PostgreSQL with SSL
RUN mkdir -p /var/run/postgresql/10-main.pg_stat_tmp; \
    chown postgres:postgres /var/run/postgresql/10-main.pg_stat_tmp -R; \
    touch /root/.rnd; \
    openssl genrsa -des3 -passout pass:supersecret -out server.key 1024; \
    openssl rsa -in server.key -passin pass:supersecret -out server.key; \
    openssl req -new -key server.key -days 3650 -out server.crt \
		-passin pass:supersecret -x509 \
		-subj '/C=US/ST=Texas/L=Austin/O=Conversion Logix/CN=clxmedia.com/emailAddress=tcc-admin@clxmedia.com'; \
    cp server.crt root.crt; \
    mv -f server.crt /var/lib/postgresql/10/main/.; \
	mv -f server.key /var/lib/postgresql/10/main/.; \
	mv -f root.crt /var/lib/postgresql/10/main/.; \
    chown postgres:postgres /var/lib/postgresql/10/main/server.key;
COPY pg_hba.conf /etc/postgresql/10/main/pg_hba.conf
COPY postgresql.conf /etc/postgresql/10/main/postgresql.conf
COPY san.cnf /etc/nginx/snippets/san.cnf

# Configure SSL for nginx
RUN mkdir -p /etc/nginx/snippets /etc/nginx/ssl/certs /etc/nginx/ssl/private; \
    openssl genrsa -out /etc/nginx/ssl/private/nginx-selfsigned.key 4096; \
    openssl req -new -sha256 -out /etc/nginx/ssl/private/private.csr \
                -key /etc/nginx/ssl/private/nginx-selfsigned.key \
                -config /etc/nginx/snippets/san.cnf \
                -subj '/C=US/ST=Texas/L=Austin/O=Conversion Logix/CN=tcc.local/emailAddress=tcc-admin@clxmedia.com'; \
    openssl x509 -req -sha256 -days 3650 \
        -in /etc/nginx/ssl/private/private.csr \
        -signkey /etc/nginx/ssl/private/nginx-selfsigned.key \
        -out /etc/nginx/ssl/certs/nginx-selfsigned.crt \
        -extensions req_ext \
        -extfile /etc/nginx/snippets/san.cnf; \
    openssl dhparam -out /etc/nginx/ssl/certs/dhparam.pem 128; \
    chmod 700 /etc/nginx/ssl/private/nginx-selfsigned.key;

COPY servers/* /etc/nginx/servers/

# Install Node 10 & yarn
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt install -y nodejs
RUN curl -o- -L https://yarnpkg.com/install.sh | bash;
RUN ln -s /root/.yarn/bin/yarn /usr/local/bin/yarn

# TCC apps setup
COPY startup_scripts/* /usr/local/bin/
COPY env.main /bengal/.env
COPY env.widget /bengal/widget/.env
COPY nginx.conf /etc/nginx/nginx.conf
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

CMD ["/usr/bin/supervisord"]