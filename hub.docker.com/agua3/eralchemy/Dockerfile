FROM python:3.7.2-alpine

RUN apk --no-cache add \
    libc-dev \
    libffi-dev \
    libressl-dev \
    ca-certificates \
    gcc \
    postgresql-dev \
    graphviz \
    graphviz-dev \
    msttcorefonts-installer

RUN update-ms-fonts && fc-cache -f

COPY requirements.txt ./

RUN pip install -r requirements.txt

COPY run.sh /run.sh

ENTRYPOINT [ "/run.sh" ]