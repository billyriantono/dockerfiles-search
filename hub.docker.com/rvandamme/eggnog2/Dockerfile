FROM python:2.7

RUN apt update && apt install -y procps && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN git clone https://github.com/jhcepas/eggnog-mapper.git /eggnog-mapper
