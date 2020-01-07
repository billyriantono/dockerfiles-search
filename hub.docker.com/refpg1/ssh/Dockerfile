FROM ubuntu:18.10

RUN apt-get update 
RUN apt-get install -y openssh-server
RUN apt-get install -y vim
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y composer
RUN apt-get install -y nodejs
RUN apt-get install -y npm yarn
RUN apt-get install -y php php-dom php-zip unzip php-mysql php-curl php-intl php-mbstring php-xmlrpc php-gd
RUN apt-get install -y rsync
RUN apt-get install -y curl
RUN apt-get install -y mysql-client
RUN apt-get install -y ncftp

RUN mkdir /var/run/sshd

ENV ROOT_PASSWORD pP2Mn387S
RUN echo "root:$ROOT_PASSWORD" | /usr/sbin/chpasswd

RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile


COPY run.sh /run.sh
RUN chmod u+x /run.sh

COPY .bash_aliases /root/.bash_aliases
COPY ssh_config /root/.ssh/config

RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
RUN chmod +x wp-cli.phar
RUN mv wp-cli.phar /usr/local/bin/wp

WORKDIR /var/www/html

EXPOSE 22
ENTRYPOINT ["/run.sh"]
CMD /usr/sbin/sshd -D
