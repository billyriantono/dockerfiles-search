FROM frolvlad/alpine-glibc:alpine-3.7_glibc-2.26

# Inspired by the following ansible and alpine sources:
# https://github.com/William-Yeh/docker-ansible/blob/master/alpine3/Dockerfile
# https://github.com/asg1612/alpine-oracle-instantclient

COPY instantclient-basic-linux.x64-12.2.0.1.0.zip instantclient_12_2.zip

RUN apk --update --no-cache add libaio && \
    unzip instantclient_12_2.zip && \
    mv instantclient_12_2/ /usr/lib/ && \
    rm instantclient_12_2.zip && \
    ln /usr/lib/instantclient_12_2/libclntsh.so.12.1 /usr/lib/libclntsh.so && \
    ln /usr/lib/instantclient_12_2/libocci.so.12.1 /usr/lib/libocci.so && \
    ln /usr/lib/instantclient_12_2/libociei.so /usr/lib/libociei.so && \
    ln /usr/lib/instantclient_12_2/libnnz12.so /usr/lib/libnnz12.so


RUN echo "===> Adding Python runtime..."  && \
    apk --update --no-cache add python py-pip openssl ca-certificates && \
    apk --update --no-cache add --virtual .build-dependencies python-dev libffi-dev openssl-dev build-base && \
    pip install --upgrade  pip cffi && \
    pip install ansible && \
    echo "===> Installing handy tools (not absolutely required)..." && \
    pip install --upgrade pywinrm cx_Oracle && \
    apk --update --no-cache add sshpass openssh-client rsync && \
    apk del .build-dependencies && \
    rm -rf /var/cache/apk/* && \
    echo "===> Adding hosts for convenience..."  && \
    mkdir -p /etc/ansible && \
    echo 'localhost' > /etc/ansible/hosts

ENV ORACLE_BASE /usr/lib/instantclient_12_2
ENV LD_LIBRARY_PATH /usr/lib/instantclient_12_2
ENV TNS_ADMIN /usr/lib/instantclient_12_2
ENV ORACLE_HOME /usr/lib/instantclient_12_2

CMD [ "ansible-playbook", "--version" ]
