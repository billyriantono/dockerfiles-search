FROM amazonlinux:2018.03
MAINTAINER Ken DeLong "kenwdelong@gmail.com"

ENV WORK="/work"
RUN curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py && \
    python get-pip.py
RUN pip install ansible==2.7.1
RUN mkdir $WORK && \
    chmod 0777 $WORK
WORKDIR $WORK
ENTRYPOINT ["ansible-playbook"]