# -*- dockerfile -*-
FROM python:2
MAINTAINER Matt Bodenhamer <mbodenhamer@mbodenhamer.com>

RUN pip install -U --no-cache \
    depman==0.3.4 \
    yatr==0.0.10

RUN mkdir -p /etc/bash_completion.d \
    && yatr --install-bash-completions > /dev/null \
    && echo "source /etc/bash_completion.d/yatr" >> /root/.bashrc \
    && mkdir -p /root/.yatr \
    && mkdir -p /root/.depman

CMD ["python2"]