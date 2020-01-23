FROM python:3.7
ARG TOX_VERSION=3.5.3
ENV TOX_VERSION=${TOX_VERSION}
RUN python3.7 -m pip install tox==${TOX_VERSION}
VOLUME /tox
WORKDIR /tox
ENTRYPOINT ["python3.7", "-m", "tox"]
