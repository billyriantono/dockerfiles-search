FROM ubuntu:14.04.5
MAINTAINER Fernando Chorney "gitlab-dockerfile@djsbx.com"

# Install python development packages, and pip
RUN apt-get update -qy
RUN apt-get install -y python-dev python-pip

# Latest version of pip
RUN pip install --upgrade pip

# Install Postgresql 9.3
RUN apt-get install -y postgresql-9.3 postgresql-server-dev-9.3

# Install PostGIS 2.1
RUN apt-get install -y postgresql-contrib-9.3 postgresql-9.3-postgis-2.1
