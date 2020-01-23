FROM jasonrivers/nagios:latest

LABEL maintainer=coen.vanleeuwen@tno.nl

RUN apt-get update && apt-get install -y ssmtp && \
	apt-get clean && rm -Rf /var/lib/apt/lists/*
