FROM python:3.7-slim-buster

WORKDIR /app

ARG SYSTEM_PACKAGES="make"

RUN apt-get -qq update
RUN apt-get -qq upgrade
RUN apt-get -qq install ${SYSTEM_PACKAGES}

COPY . /app

RUN pip install --upgrade pip
RUN pip install --upgrade wheel setuptools twine pipenv
RUN pipenv install --dev --system --deploy

RUN apt-get clean autoclean && \
    apt-get autoremove --yes && \
    rm -rf /var/lib/{apt,dpkg,cache,log}/

ARG BUILD_DATETIME
ARG SHA1
ARG VERSION

LABEL io.github.mbeacom.description="CloudEndure CLI and API client module" \
    io.github.mbeacom.documentation="https://mbeacom.github.io/cloudendure-python/" \
    io.github.mbeacom.licenses="MIT" \
    io.github.mbeacom.image.revision=$SHA1 \
    io.github.mbeacom.image.version=$VERSION \
    io.github.mbeacom.image.vendor="mbeacom" \
    io.github.mbeacom.image.source="https://github.com/mbeacom/cloudendure-python" \
    io.github.mbeacom.image.title="CloudEndure Client" \
    io.github.mbeacom.image.created=$BUILD_DATETIME
