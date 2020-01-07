FROM asgard/openblas:py3

# Python 3
RUN apt-get update && apt-get install -y \
  python3 python3-dev python3-pip python3-setuptools \
  libssl-dev libffi-dev

# set alias for python3 => python
RUN ln -s /usr/bin/python3 /usr/bin/python && \
    ln -s /usr/bin/pip3 /usr/bin/pip

RUN pip install -U pip && \
  pip install --no-cache-dir cython && \
  pip install --no-cache-dir numpy && \
  pip install --no-cache-dir scipy

# # lxml
# RUN apt-get install -y \
#   libxml2-dev \
#   libxslt1-dev \
#   python-lxml

# Clean up APT when done.
RUN apt-get autoremove -y && \
  apt-get clean -y && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Init script
ENTRYPOINT ["/sbin/my_init"]
