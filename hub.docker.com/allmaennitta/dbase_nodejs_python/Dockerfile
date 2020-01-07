FROM allmaennitta/dbase_nodejs:latest
LABEL maintainer.name="Ingo Beyerlein, allmännITta"
LABEL maintainer.mail="ingo.beyerlein@allmaennitta.de"


########## PATHS ##########

########## VERSIONS ##########
ENV PY_VERSION=2.7
########## SET UP ##########

########## MAIN ##########

RUN apt-get update \
    && apt install -y software-properties-common \
    && add-apt-repository ppa:jonathonf/python-${PY_VERSION} \
    && apt update \
    && apt install -y python${PY_VERSION} python${PY_VERSION}-dev python-virtualenv \
    && curl -O https://bootstrap.pypa.io/get-pip.py \
    && python${PY_VERSION} get-pip.py

RUN unlink /usr/bin/python \
    && ln -s /usr/bin/python${PY_VERSION} /usr/bin/python

########## CLEAN UP ##########
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && apt autoremove -y \
    && apt clean \
    && rm  get-pip.py


CMD bash


