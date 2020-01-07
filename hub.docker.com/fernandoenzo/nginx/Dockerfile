FROM fernandoenzo/debian:testing-min
MAINTAINER Fernando Enzo Guarini (fernandoenzo@gmail.com)

COPY scripts/basics /tmp
COPY scripts/boot /usr/local/
COPY static/bash_history /root/.bash_history

RUN bash /tmp/basics
COPY static/default.template /etc/nginx/sites-available

EXPOSE 80
EXPOSE 443
