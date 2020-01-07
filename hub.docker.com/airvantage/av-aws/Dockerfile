FROM airvantage/av-debian

MAINTAINER gmorice@sierrawireless.com

RUN echo "update system and install needed deps" \
    && apt-get -y -qq --force-yes update \
    && apt-get -y -qq --force-yes install python wget unzip \
    && echo "install aws" \
    && wget -P /tmp http://s3.amazonaws.com/aws-cli/awscli-bundle.zip \
    && unzip /tmp/awscli-bundle.zip -d /tmp \
    && /tmp/awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws \
    && echo "add user" \
    && useradd -ms /bin/bash av-user \
    && cd && cp -R .bashrc .profile  /home/av-user \
    && echo "clean up" \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

USER av-user

ENTRYPOINT ["/usr/local/bin/aws"]
