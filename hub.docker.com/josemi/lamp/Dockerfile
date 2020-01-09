FROM ubuntu:18.04

EXPOSE 22 80

RUN apt-get update && \
    apt-get -y install software-properties-common && \
    apt-add-repository -y ppa:ansible/ansible && \
    apt-get update && \
    apt-get -y upgrade && \
    apt-get install -y git curl ansible && \
    mkdir /opt/ansible

ADD ansible /opt/ansible

WORKDIR /opt/ansible

RUN ansible-playbook playbook.yml --extra-vars "name=developer password=developer drush_version=8.1.17 coder_version=8.x-2.x"

RUN rm -rf /opt/ansible

WORKDIR /var/www/html

VOLUME ["/var/log/apache2","/var/log/supervisor","/var/log/mysql","/var/lib/mysql"]

CMD ["/usr/bin/supervisord"]