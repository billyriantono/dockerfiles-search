FROM debian:stretch

MAINTAINER ReanGD

ENV DEBIAN_FRONTEND noninteractive

ADD * /home/
ADD https://deb.nodesource.com/setup_6.x /home/setup_6.sh

RUN chmod +x /home/clean.sh && \
    chmod +x /home/run.sh && \
    chmod +x /home/setup_6.sh && \
    \
    echo en_US.UTF-8 UTF-8 > /etc/locale.gen && \
    echo ru_RU.UTF-8 UTF-8 >> /etc/locale.gen && \
    \
    apt-get update && \
    apt-get install -y --no-install-recommends locales git openssh-server openjdk-8-jdk less nano wget zip gnupg && \
    apt-get install -y --no-install-recommends python3-pip python3-setuptools gettext && \
    \
    /home/setup_6.sh && \
    apt-get install -y nodejs && \
    \
    pip3 install -r /home/requirements.txt && \
    pip3 install -e git+git://github.com/kmmbvnr/django-jenkins.git#egg=django-jenkins && \
    \
    npm install -g bower && \
    npm install -g cloc && \
    npm install -g jshint && \
    npm install -g csslint && \
    npm install -g eslint && \
    npm install -g babel-core && \
    npm install -g babel-loader && \
    npm install -g babel-preset-es2015 && \
    npm install -g babel-preset-stage-0 && \
    npm install -g babel-runtime && \
    npm install -g webpack && \
    npm install -g gulp-cli && \
    npm install -g gulp-order && \
    npm install -g node-gyp && \    
    npm install -g node-sass && \
    \
    useradd -m jenkins && \
    echo "jenkins:jenkins" | chpasswd && \
    mkdir -p /jenkins && \
    \
    mkdir /var/run/sshd/ && \
    sed 's/UsePAM yes/UsePAM no/' -i /etc/ssh/sshd_config && \
    /home/clean.sh

ENV LANG ru_RU.UTF-8
ENV LANGUAGE ru_RU.UTF-8

EXPOSE 22

VOLUME ["/jenkins"]

CMD /home/run.sh
