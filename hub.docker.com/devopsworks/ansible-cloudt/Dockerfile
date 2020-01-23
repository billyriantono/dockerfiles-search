FROM devopsftw/baseimage:0.4.0

RUN add-apt-repository ppa:jonathonf/python-3.6 \
    && apt-get update -qq \
    && apt-get install -y python3.6 \
    && curl https://bootstrap.pypa.io/get-pip.py | python3.6 \
    && pip3 install pipenv \
    && rm -rf /var/lib/apt/lists/* /root/.cache
