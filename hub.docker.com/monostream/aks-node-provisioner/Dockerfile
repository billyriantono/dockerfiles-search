FROM williamyeh/ansible:alpine3

ENV ANP_PLAYBOOK="/etc/ansible/playbook/playbook.yml"
ENV ANP_CONFIGMAP_VOLUME="/etc/ansible/playbook"

RUN apk add --no-cache inotify-tools

COPY ansible-watch-playbook.sh .
RUN chmod u+x ansible-watch-playbook.sh

CMD ["./ansible-watch-playbook.sh"]
