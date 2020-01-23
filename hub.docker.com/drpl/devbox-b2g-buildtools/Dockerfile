FROM drpl/devbox-x11:latest

MAINTAINER Luca Greco <luca.greco@alcacoop.it>

# import provisioning assets
ADD B2G-prepare.sh /usr/local/src/

# run provisioning
RUN sh /usr/local/src/B2G-prepare.sh && \
    ansible-playbook /etc/ansible/playbooks/devbox-base/cleanup.yml -c local
