## -*- docker-image-name: "xdevdavinci/python3.6" -*-

FROM xdevdavinci/base

RUN apt-get update && apt-get install -y \
        python3.6 \
        python3.6-dev \
        python3-pip \
        python3-setuptools \
        mysql-client && \
        apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV PYTHON python3.6

RUN python3 -m pip install ipdb

RUN pip3 install --upgrade "setuptools" "pip" && rm -rf /root/.cache

CMD [ "node" ]
