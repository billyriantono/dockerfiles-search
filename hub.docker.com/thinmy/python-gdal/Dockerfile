FROM python:3.6

ENV PYTHONUNBUFFERED 1

RUN apt-get update -y \
    && apt-get -y install \
        binutils \
        libproj-dev \
        gdal-bin \
    && bash -c "rm -rf /var/lib/apt/lists/*"