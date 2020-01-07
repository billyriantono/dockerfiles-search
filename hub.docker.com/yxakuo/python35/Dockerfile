FROM python:3.5

MAINTAINER Allen tGuo

USER root

ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN mv /etc/apt/sources.list /etc/apt/sources.list.BackuP
COPY files/sources.list.jessie /etc/apt/sources.list

RUN mkdir -p ~/.pip \
    && touch ~/.pip/pip.conf \
    && echo "[global]" > ~/.pip/pip.conf \
    && echo "index-url = https://pypi.douban.com/simple" >> ~/.pip/pip.conf \
    && echo "[install]" >> ~/.pip/pip.conf \
    && echo "use-mirrors = true" >> ~/.pip/pip.conf \
    && pip install --upgrade pip

CMD ["python3"]

