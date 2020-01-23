FROM	httpd:latest
MAINTAINER Denis Lemire <denis.lemire@distributel.ca

RUN     apt-get -yqq update && \
        apt-get install -yq --no-install-recommends bsdmainutils

CMD	["httpd-foreground"]
