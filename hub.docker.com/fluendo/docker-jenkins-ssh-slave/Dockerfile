FROM jenkins/ssh-slave

MAINTAINER fluendo

ENV DEBIAN_FRONTEND noninteractive

# Add i386 architecture for wine purpose if necessary.
RUN dpkg --add-architecture i386

# Install required packages
RUN apt-get update && \
    apt-get upgrade -y

# Install git
RUN apt-get install -y git

# Install Python3.5
RUN apt-get install -y \
        python3.5 \
        python3.5-dev \
        python3-setuptools \
        python3-pip
RUN python3 -m pip install -U pip setuptools requests tinys3 lxml junit-xml jira six

# Missing bootstrap packages
RUN apt-get install -y autotools-dev automake libtool cmake bison flex texinfo doxygen \
                       yasm pkg-config gtk-doc-tools \
                       libxv-dev libpulse-dev python-dev libxi-dev \
                       x11proto-record-dev libxrender-dev libgl1-mesa-dev libxfixes-dev libxdamage-dev \
                       libxcomposite-dev libasound2-dev libxml-simple-perl debhelper \
                       devscripts transfig gperf libdbus-glib-1-dev libgtk2.0-dev \
                       glib-networking-common subversion wine curl rpm vim nuget

# Install dotnet
RUN apt-get install gpg -y && \
    wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.asc.gpg && \
    mv microsoft.asc.gpg /etc/apt/trusted.gpg.d/ && \
    wget -q https://packages.microsoft.com/config/debian/9/prod.list && \
    mv prod.list /etc/apt/sources.list.d/microsoft-prod.list && \
    chown root:root /etc/apt/trusted.gpg.d/microsoft.asc.gpg && \
    chown root:root /etc/apt/sources.list.d/microsoft-prod.list && \
    apt-get install apt-transport-https && \
    apt-get update && \
    apt-get install dotnet-sdk-2.2 -y
    
    
# Install ldap support
RUN apt-get install -y sudo wget libnss-ldap

#Install nuget dependencies
RUN curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/v5.1.0/nuget.exe
RUN echo "alias nuget='mono /usr/local/bin/nuget.exe'" >> ~/.bashrc
RUN apt-get install libmono-system-net-http4.0-cil && \
    apt install libmono-system-io-compression-filesystem4.0-cil -y

#Install bdd tools
RUN pip install behave
RUN pip3 install PYhamcrest aiohttp Pillow numpy

#Install hbbtv tools
RUN apt install -y apt-transport-https lsb-release ca-certificates
RUN wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
RUN apt update
RUN apt install -y php7.0 php7.0-cli php7.0-common

COPY ./run.sh .
COPY ./apt-get /usr/local/sbin/apt-get
RUN chmod +x /usr/local/sbin/apt-get

# Entrypoint definition
ENTRYPOINT ["./run.sh"]
