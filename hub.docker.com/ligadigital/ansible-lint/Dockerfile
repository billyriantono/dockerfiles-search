FROM python:3

LABEL Name=ansible-lint Version=latest

WORKDIR /run
RUN pip install --no-cache-dir ansible-lint


RUN \
      echo '#!/bin/bash'            >  /run.sh && \
      echo 'ansible-lint $PLAYBOOK' >> /run.sh
RUN chmod +x /run.sh

ENV PLAYBOOK=playbook.yml

CMD [ "/run.sh" ]

