FROM ventx/alpine

RUN apk --update add wget ca-certificates py2-pip python2-dev py2-cffi openssl-dev gcc make g++ tzdata dateutils && \
pip install jmespath pyOpenSSL ansible==2.4 

RUN mkdir /etc/ansible && echo "localhost ansible_connection=local" > /etc/ansible/hosts

CMD ["/bin/bash"]
