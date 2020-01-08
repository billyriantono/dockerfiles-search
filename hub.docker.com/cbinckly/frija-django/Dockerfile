# pull official base image
FROM cbinckly/frija:latest as builder

FROM python:3.7-alpine
# set environment varibles
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

RUN apk add --no-cache \
        --upgrade \
        --repository http://dl-cdn.alpinelinux.org/alpine/edge/main \
        gettext \
        libpq \
        postgresql-client \
        && rm -rf /var/cache/apk/*

# set work directory
WORKDIR /usr/src/app
COPY --from=builder /wheels /wheels

# install dependencies
RUN pip install --upgrade pip \
    && pip install -r /wheels/requirements.txt -f /wheels \
    && rm -rf /root/.cache/pip/*

# copy project
COPY . /usr/src/app/
