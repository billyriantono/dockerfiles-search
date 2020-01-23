FROM fastsol/lap7

RUN apt-get update && \
apt-get install php-xdebug -y && \
apt-get clean -y && apt-get autoclean -y && apt-get autoremove -y && \
rm -rf /var/cache/debconf/*-old && rm -rf /var/lib/apt/lists/* && rm -rf /usr/share/doc/*
