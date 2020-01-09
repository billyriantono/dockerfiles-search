FROM python:slim-stretch
LABEL AUTHOR="dalongrong"
LABEL EMAIL="1141591465@qq.com"
WORKDIR /app
RUN apt-get update && apt-get install -y  --reinstall build-essential \
    && pip install circus  chaussette \
    && apt-get remove -y --purge build-essential \
    && rm -rf /var/lib/apt/lists/*
COPY circus.ini  /app/
COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
ENTRYPOINT [ "/entrypoint.sh" ]