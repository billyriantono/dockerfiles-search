FROM dongyg/i3shell

RUN \
    DEBIAN_FRONTEND=noninteractive \
    apt-get -q -y update && \
    apt-get -q -y install fcgiwrap

RUN pip install --no-cache-dir flup==1.0.2
