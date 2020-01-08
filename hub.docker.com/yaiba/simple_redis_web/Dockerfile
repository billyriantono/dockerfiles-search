# DESCRIPTION: alpine simple web with redis backend

FROM alpine:3.3
MAINTAINER Yaiba

RUN apk --update add \
        python \
        python-dev \
        py-pip \
        build-base \
				redis \
    && rm -rf /var/cache/apk/*

ENV HOME /app
WORKDIR $HOME

COPY . $HOME
RUN pip install -r $HOME/requirements.txt

EXPOSE 8080
CMD ["python", "demo.py"]
