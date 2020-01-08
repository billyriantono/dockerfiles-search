# Benutzen Sie folgenden Befehl, um ein lokales Image von diesem Dockerfile zu erzeugen:
#   docker build -t local-docker-dev-debian-phoenix:wholesale-api .


# elixir (Stand: 09.08.2018 - Version: 1.7.2)
FROM elixir:1.7.2
MAINTAINER Richard-Mueller <dev@richard-mueller.de>
ENV REFRESHED_AT 09-08-2018


# phoenix (Stand: 24.01.2018 - Version: phx_new.ez)
ENV PHOENIX_VERSION phx_new.ez

# # <! ACHTUNG: Die folgenden 4 Zeilen einkommentieren, wenn Assets benutzt werden>
# # node (Stand: 24.01.2018 - Version: 8)
# ENV NODE_VERSION 8


# Quellen:
# https://docs.microsoft.com/de-de/sql/connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server?view=sql-server-2017

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get -y install apt-utils apt-transport-https wget
RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
RUN curl https://packages.microsoft.com/config/debian/9/prod.list > /etc/apt/sources.list.d/mssql-release.list
RUN apt-get update && DEBIAN_FRONTEND=noninteractive ACCEPT_EULA=Y apt-get -y install msodbcsql17 mssql-tools unixodbc-dev locales postgresql-client

# setze locale + installiere postgresql-client
RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    dpkg-reconfigure --frontend=noninteractive locales && \
    update-locale LANG=en_US.UTF-8
ENV LANG en_US.UTF-8

# hex installieren
RUN mix local.hex --force

# rebar installieren
RUN mix local.rebar --force

# phoenix installieren (Stand: 24.01.2018 - Version: phx_new.ez)
RUN mix archive.install https://github.com/phoenixframework/archives/raw/master/$PHOENIX_VERSION --force

# # <! ACHTUNG: Die folgenden 4 Zeilen einkommentieren, wenn Assets benutzt werden>
# # node installieren
# RUN curl -sL https://deb.nodesource.com/setup_$NODE_VERSION.x -o nodesource_setup.sh
# RUN bash nodesource_setup.sh
# RUN apt-get install nodejs
