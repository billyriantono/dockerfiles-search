# escape=`
FROM williamyeh/ansible:alpine3

LABEL version="1.0"
LABEL maintainer="Bill Westhead"
LABEL description="A base command image for Ansible."

ENV PLAYBOOK      playbook.yml
ENV INVENTORY     hosts

RUN mkdir /lmport
WORKDIR /lmport

ENTRYPOINT ["ansible"]
CMD ["--version"]
