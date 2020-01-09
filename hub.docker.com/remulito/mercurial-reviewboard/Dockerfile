FROM python:2

LABEL maintainer="remulito@yandex.ru"
ADD https://bitbucket.org/kedder/mercurial-reviewboard/get/default.tar.gz /tmp/mercurial-reviewboard.tar.gz
COPY requirements.txt /tmp/requirements.txt
COPY hg.ini /root/.hgrc
RUN pip install --no-cache-dir -r /tmp/requirements.txt \
    && tar -xvf /tmp/mercurial-reviewboard.tar.gz -C /tmp/ \
    && mv /tmp/kedder-mercurial-reviewboard* /root/kedder-mercurial-reviewboard \
    && rm -f /tmp/*

ENTRYPOINT [ "bash" ]
