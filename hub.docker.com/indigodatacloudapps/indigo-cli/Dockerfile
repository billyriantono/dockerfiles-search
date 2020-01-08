# docker build --rm -t indigo-cli .
FROM lipcomputing/ansible-centos7
MAINTAINER Mario David <mariojmdavid@gmail.com>
LABEL description="Indigo-DataCloud client tools"

ENV UDIR /home/client
RUN mkdir -p $UDIR
WORKDIR $UDIR

RUN ansible-galaxy install git+https://github.com/indigo-dc/ansible-role-indigo-repo.git && \
    ansible-galaxy install git+https://github.com/LIP-Computing/ansible-role-os-cli.git && \
    ansible-playbook /etc/ansible/roles/ansible-role-os-cli/tests/test.yml && \
    ansible-playbook /etc/ansible/roles/ansible-role-indigo-repo/tests/test.yml && \
    yum -y install indigodc-release && \
    yum -y update && \
    yum -y install orchent wattson

