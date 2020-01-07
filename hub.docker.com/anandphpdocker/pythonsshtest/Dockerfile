FROM python:3.6-slim
LABEL maintainer="joona.hook@visma.com"

#COPY ./database/odbcinst.ini /odbcinst.ini
#COPY ./database/odbcinst.ini /etc/odbcinst.ini

COPY . /home/site/wwwroot

# Web Site Home
ENV HOME_SITE "/home/site/wwwroot"

WORKDIR ${HOME_SITE}


RUN apt-get update -y
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        libpq-dev \
        openssh-server \
        vim \
        curl \
        wget \
        tcptraceroute
RUN apt-get install -y --no-install-recommends apt-utils
RUN apt-get -o Dpkg::Options::="--force-confdef" -o Dpkg::Options::="--force-confold" install -y --no-install-recommends build-essential
RUN apt-get -o Dpkg::Options::="--force-confdef" -o Dpkg::Options::="--force-confold" install -y --no-install-recommends unixodbc
RUN apt-get install -y --no-install-recommends unixodbc-dev
RUN apt-get install -y --no-install-recommends freetds-dev
RUN apt-get install -y --no-install-recommends tdsodbc
RUN apt-get install -y --no-install-recommends freetds-bin
RUN apt-get install -y --no-install-recommends vim

RUN pip install --ignore-installed -r requirements.txt

RUN apt-get purge -y --auto-remove build-essential unixodbc-dev freetds-dev

RUN chmod 554 /usr/lib/x86_64-linux-gnu/odbc/libtdsodbc.so

EXPOSE 80 2222

HEALTHCHECK --interval=5s --timeout=5s CMD curl --fail http://localhost:80 || exit 1

# setup SSH
RUN mkdir -p /home/LogFiles \
     && echo "root:Docker!" | chpasswd \
     && echo "cd /home" >> /etc/bash.bashrc 

COPY sshd_config /etc/ssh/
RUN mkdir -p /opt/startup
COPY init_container.sh /opt/startup/init_container.sh


# configure startup
RUN chmod -R 777 /opt/startup
ENTRYPOINT ["/opt/startup/init_container.sh"]
