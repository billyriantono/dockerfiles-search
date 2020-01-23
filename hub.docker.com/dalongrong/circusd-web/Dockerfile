FROM python:2.7-slim-stretch
LABEL AUTHOR="dalongrong"
LABEL EMAIL="1141591465@qq.com"
RUN apt-get update && apt-get install -y  --reinstall build-essential \
    && pip install  circus-web  \
    && pip uninstall -y tornado  \
    && pip uninstall -y pyzmq  \
    && pip install tornado==3.2.2 \
    && pip install pyzmq==16.0.4 \
    && apt-get remove -y --purge build-essential \
    && rm -rf /var/lib/apt/lists/*
COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
ENTRYPOINT [ "/entrypoint.sh" ]