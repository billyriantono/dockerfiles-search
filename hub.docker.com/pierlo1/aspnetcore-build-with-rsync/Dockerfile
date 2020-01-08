FROM microsoft/aspnetcore-build:1.1.2

LABEL maintainer=pierregordon@protonmail.com

RUN apt-get update && \
    apt-get install -y --no-install-recommends rsync && \
    apt-get autoremove -y && \
    apt-get clean && \
    rm -rf /var/tmp/* && \
    rm -rf /tmp/*
