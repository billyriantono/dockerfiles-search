FROM python:3.7-slim

RUN apt-get update && apt-get install --no-install-recommends -y \
        curl \
        tar \
        git \
        fish \
        sudo \
        libxext6 \
        libxrender1 \
        libxtst6 \
        libfreetype6 \
        libfontconfig1 \
    && rm -rf /var/lib/apt/lists/* \
    && useradd -ms /usr/bin/fish developer \
    && echo "developer ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

WORKDIR /opt/pycharm

RUN curl -fsSL https://download.jetbrains.com/python/pycharm-professional-2018.3.2.tar.gz -o /opt/pycharm/pycharm.tar.gz \
    && tar xvzf pycharm.tar.gz --strip-components=1 \
    && chown -R developer:developer  /opt/pycharm \
    && rm pycharm.tar.gz

USER developer

SHELL ["/usr/bin/fish", "-c"]
CMD [ "/opt/pycharm/bin/pycharm.sh" ]