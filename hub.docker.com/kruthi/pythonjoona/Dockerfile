FROM python:3.6-slim
LABEL maintainer="joona.hook@visma.com"

COPY ./dist/salescaseprediction /home/site/wwwroot

# Web Site Home
ENV HOME_SITE "/home/site/wwwroot"

WORKDIR ${HOME_SITE}

RUN apt-get update -y 
RUN apt-get update \  
&& apt-get install -y --no-install-recommends \
        libpq-dev \
        openssh-server \
        curl \
        wget \
        tcptraceroute \
		&& echo "root:Docker!!!*" | chpasswd \
     && echo "cd /home" >> /etc/bash.bashrc 
RUN apt-get install -y --no-install-recommends apt-utils
RUN apt-get install -y curl wget gnupg
RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
RUN apt-get -o Dpkg::Options::="--force-confdef" -o Dpkg::Options::="--force-confold" install -y --no-install-recommends build-essential
RUN apt-get -o Dpkg::Options::="--force-confdef" -o Dpkg::Options::="--force-confold" install -y --no-install-recommends unixodbc
RUN apt-get install -y --no-install-recommends unixodbc-dev
RUN apt-get install -y --no-install-recommends vim

RUN TEMP_DEB="$(mktemp)" \
 && wget -O "$TEMP_DEB" 'https://packages.microsoft.com/debian/9/prod/pool/main/m/msodbcsql17/msodbcsql17_17.2.0.1-1_amd64.deb' \
 && yes | dpkg --skip-same-version -i "$TEMP_DEB" \
 && rm -f "$TEMP_DEB"

RUN pip install --ignore-installed -r requirements.txt
RUN apt-get purge -y --auto-remove build-essential unixodbc-dev



# setup SSH
RUN mkdir -p /home/LogFiles

COPY sshd_config /etc/ssh/
RUN mkdir -p /opt/startup
COPY init_container.sh /opt/startup/init_container.sh

# configure startup
RUN chmod -R 777 /opt/startup
EXPOSE 80 2222
ENTRYPOINT ["/opt/startup/init_container.sh"]

