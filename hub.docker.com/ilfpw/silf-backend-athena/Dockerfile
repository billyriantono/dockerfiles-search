FROM python:3.7

ARG REQIREMENTS_FILE=base.txt
ENV PYTHONPATH=/athena/src

RUN apt-get update && \
    apt-get upgrade -qy && \
    apt-get install -y libyaml-dev libhunspell-dev libxml2-dev libxslt-dev python-jinja2 hunspell-pl hunspell-en-us && \
    pip3 install jinja2 && \
    apt-get autoremove -y && apt-get clean && rm -rf /var/cache/* && rm -rf /var/tmp/* && rm -rf /tmp/*

WORKDIR /athena

COPY requirements /athena/requirements
RUN pip3 install -r requirements/${REQIREMENTS_FILE}

COPY . /athena

CMD ["./scripts/docker_start.sh"]
