FROM            jenkins:latest
MAINTAINER      Inonit AS <support@inonit.no>

#
# Install build dependencies
#
USER            root

# Add a PPA that hosts python3.5
RUN             echo "deb http://ppa.launchpad.net/fkrull/deadsnakes/ubuntu trusty main" > /etc/apt/sources.list.d/deadsnakes.list
RUN             echo "deb-src http://ppa.launchpad.net/fkrull/deadsnakes/ubuntu trusty main" >> /etc/apt/sources.list.d/deadsnakes.list
RUN             gpg --keyserver keyserver.ubuntu.com --recv-keys DB82666C
RUN             gpg --export DB82666C | apt-key add -

RUN             apt-get update && apt-get upgrade -y
RUN             apt-get install -y --no-install-recommends \
                  build-essential \
                  python2.7 \
                  python2.7-dev \
                  python-virtualenv \
                  python3.4 \
                  python3.4-dev \
                  python3.5 \
                  python3.5-dev \
                  nodejs \
                  npm
RUN             apt-get purge -y --auto-remove
RUN             rm -rf /var/lib/apt/lists/*


#
# Drop back to the jenkins user
#
USER            jenkins
