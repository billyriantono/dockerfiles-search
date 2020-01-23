FROM python:2.7.14-jessie
ENV REFRESHED_AT 2018-02-19
RUN apt-get update
RUN pip install boofuzz==0.0.11

# The following are only for troubleshooting and not permanent
RUN apt-get install -yqq \
	emacs \
	iputils-ping \
	wget \
	netcat

# Install ifconfig

# Port Used by Web Server
EXPOSE 26000
# Port Used by Procmon
EXPOSE 26002

WORKDIR /home
CMD /bin/bash