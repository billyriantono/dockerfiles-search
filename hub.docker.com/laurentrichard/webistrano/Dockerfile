FROM ruby:1.9
MAINTAINER Laurent RICHARD easylo@gmail.com

ENV DATA_DIR /opt/data

RUN export DEBIAN_FRONTEND="noninteractive"
RUN apt-get update \
    && apt-get install -y debconf-utils
RUN echo "postfix postfix/mailname string webistrano.dev" | debconf-set-selections
RUN echo "postfix postfix/main_mailer_type string 'Internet Site'" | debconf-set-selections

RUN apt-get update \
 && apt-get install -y mysql-client postfix rsync \
 && rm -rf /var/lib/apt/lists/*


 # ssh key
RUN mkdir -p /home/lafourchette/.ssh
COPY ./ssh/id_rsa /home/lafourchette/.ssh/id_rsa
RUN chmod 600 /home/lafourchette/.ssh/id_rsa
# for root
RUN mkdir -p /root/.ssh
COPY ./ssh/id_rsa /root/.ssh/id_rsa
RUN chmod 600 /root/.ssh/id_rsa
RUN ssh-keyscan github.com >> /root/.ssh/known_hosts


RUN git clone https://github.com/easylo/webistrano.git /opt/webistrano

#COPY src /opt/webistrano

WORKDIR /opt/webistrano
RUN bundle install
#--path vendor/bundler --without test

COPY ./entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
CMD ["app:start"]

EXPOSE 3000
VOLUME ["/opt/data"]
