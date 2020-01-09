# Use an official Python runtime as a parent image
FROM debian:stable

# bypass the "debconf: unable to initialize frontend: Dialog" problem
ENV DEBIAN_FRONTEND noninteractive

LABEL maintainer = "t.defise@gmail.com"

# Set the working directory to /app
# WORKDIR /app

# Copy the current directory contents into the container at /app
# COPY . /app

# Install any needed packages specified in requirements.txt
RUN apt-get update --yes && apt-get install --yes --no-install-recommends bind9=1:9.10.3.dfsg.P4-12.3+deb9u4 wget=1.18-5+deb9u2 ca-certificates=20161130+nmu1+deb9u1 cron=3.0pl1-128+deb9u1 mktemp=8.26-3 \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

COPY named.conf.options /etc/bind/named.conf.options 
COPY named.conf.blocked /etc/bind/named.conf.blocked
COPY named.conf /etc/bind/named.conf
COPY db.blocked /etc/bind/db.blocked

COPY generate-zonefile.sh generate-zonefile.sh

RUN chmod +x generate-zonefile.sh
RUN ./generate-zonefile.sh

COPY cron.txt cron.txt
#install new cron file
RUN crontab cron.txt
RUN rm cron.txt

# Define environment variable
# ENV NAME World

# Make port 53 available to the world outside this container
EXPOSE 53/tcp
EXPOSE 53/udp

CMD ["/usr/sbin/named", "-g"]

