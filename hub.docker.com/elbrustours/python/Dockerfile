FROM elbrustours/ubuntu

ENV PYTHON_VERSION=3.6

WORKDIR /opt/python

COPY ./requirements.txt /opt/python

# Install.
RUN echo "deb http://ppa.launchpad.net/jonathonf/python-${PYTHON_VERSION}/ubuntu xenial main" >> /etc/apt/sources.list && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 4AB0F789CBA31744CC7DA76A8CF63AD3F06FC659 && \
    apt-get update -qq && \
    apt-get install -yq --no-install-recommends python${PYTHON_VERSION} && \
    ln -sf /usr/bin/python${PYTHON_VERSION} /usr/bin/python && ln -sf /usr/bin/python${PYTHON_VERSION} /usr/bin/python3 && \
    curl https://bootstrap.pypa.io/get-pip.py | python${PYTHON_VERSION} && \
    pip install -r requirements.txt && \
    rm -rf /var/lib/apt/lists/*

# Define default command.
CMD ["python"]