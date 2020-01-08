FROM dclong/xubuntu:18.04

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        nodejs npm \
    && apt-get autoremove \
    && apt-get autoclean

