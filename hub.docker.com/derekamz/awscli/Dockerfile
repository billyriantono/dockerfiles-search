FROM derekamz/python:2.7
RUN apt update && apt install -y --no-install-recommends libyaml-dev  \
    && rm -rf /var/lib/apt/lists/* \
    && pip install six \
    && pip install --upgrade awscli
