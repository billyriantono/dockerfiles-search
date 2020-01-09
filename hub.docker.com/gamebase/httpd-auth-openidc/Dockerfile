FROM httpd:latest
RUN apt update && apt install -y libapache2-mod-auth-openidc ca-certificates && rm -rf /var/lib/apt/lists/*
RUN cp /usr/lib/apache2/modules/mod_auth_openidc.so /usr/local/apache2/modules/mod_auth_openidc.so
