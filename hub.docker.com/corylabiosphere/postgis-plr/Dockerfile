#--------- Generic stuff all our Dockerfiles should start with so we get caching ------------
FROM debian:stable
MAINTAINER Tim Sutton<tim@kartoza.com>

RUN  export DEBIAN_FRONTEND=noninteractive
ENV  DEBIAN_FRONTEND noninteractive
RUN  dpkg-divert --local --rename --add /sbin/initctl

RUN apt-get -y update; apt-get -y install gnupg2 wget ca-certificates rpl pwgen software-properties-common

RUN sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ stretch-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -

#-------------Application Specific Stuff ----------------------------------------------------

# We add postgis as well to prevent build errors (that we dont see on local builds)
# on docker hub e.g. "The following packages have unmet dependencies"
RUN apt-get update
RUN apt-get update; apt-get install -y postgresql-client-11 postgresql-common postgresql-11 postgresql-11-postgis-2.5 postgresql-11-pgrouting netcat r-base libudunits2-dev libgdal-dev libgeos-dev libproj-dev postgresql-11-plr nano

# Packages for R
RUN Rscript -e 'install.packages(c("rgdal","sf","sp"), repos="https://cran.rstudio.com",dependencies=TRUE)'

# Open port 5432 so linked containers can see them
EXPOSE 5432

# Run any additional tasks here that are too tedious to put in
# this dockerfile directly.
ADD env-data.sh /env-data.sh
ADD setup.sh /setup.sh
RUN chmod +x /setup.sh
RUN /setup.sh

# We will run any commands in this when the container starts
ADD docker-entrypoint.sh /docker-entrypoint.sh
ADD setup-conf.sh /
ADD setup-database.sh /
ADD setup-pg_hba.sh /
ADD setup-replication.sh /
ADD setup-ssl.sh /
ADD setup-user.sh /
RUN chmod +x /docker-entrypoint.sh

ENTRYPOINT /docker-entrypoint.sh