FROM ansible/ubuntu14.04-ansible:stable

RUN mkdir -p /provisioning
ADD files/provision /bin/
RUN chmod a+x /bin/provision

RUN ansible-galaxy install willshersystems.sshd lcacciagioni.supervisord jcsaaddupuy.supervisord_config
ADD files/ansible.yml /provisioning/

RUN provision

EXPOSE 22
CMD /usr/bin/supervisord -c /etc/supervisor/supervisord.conf -n