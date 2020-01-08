FROM mongo:4.0.4
MAINTAINER Thorsten Steube <tsteube@gmx.de>

#RUN localedef -i de_DE -c -f UTF-8 -A /usr/share/locale/locale.alias de_DE.UTF-8
#ENV LANG de_DE.utf8

COPY mongo-initdb.d /docker-entrypoint-initdb.d

