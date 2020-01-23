FROM python:3.7-stretch
LABEL maintainer="chriskshealy@gmail.com"
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        postgresql-client \
    && rm -rf /var/lib/apt/lists/*
RUN mkdir /usr/src/dataset && \
    mkdir -p /var/log/email-parser
WORKDIR /usr/src/app
COPY /app .
RUN pip install --no-cache-dir -r requirements.txt
COPY docker-entrypoint.sh /usr/local/bin/.
RUN chmod 755 /usr/local/bin/docker-entrypoint.sh
ENTRYPOINT ["sh",  "/usr/local/bin/docker-entrypoint.sh"]
