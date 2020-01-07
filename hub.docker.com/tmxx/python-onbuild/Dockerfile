FROM tmxx/python:3.5

ONBUILD ARG requirements="-r requirements.txt"
ONBUILD COPY . /app
ONBUILD RUN apk --no-cache add --virtual build-dependencies \
                build-base \
                linux-headers \
                libxml2-dev \
                libxslt-dev \
                python3-dev==$PYTHON_VERSION && \
              pip --no-cache-dir --disable-pip-version-check install \
                $requirements && \
            apk --no-cache del build-dependencies

WORKDIR /app
ENV PYTHONPATH /app
