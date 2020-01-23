FROM ansible/ubuntu14.04-ansible:stable

ADD ansible /srv/example
WORKDIR /srv/example

RUN ansible-playbook site.yml -c local
EXPOSE 80
ENTRYPOINT ["/usr/local/bin/apachectl", "-DFOREGROUND"]
