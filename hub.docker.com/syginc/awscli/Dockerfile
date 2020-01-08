FROM python:3.7

RUN curl -s -L -o /usr/local/bin/jq https://github.com/stedolan/jq/releases/download/jq-1.6/jq-linux64 && \ 
    chmod +x /usr/local/bin/jq && \
    pip install --no-cache-dir --upgrade awscli pipenv
