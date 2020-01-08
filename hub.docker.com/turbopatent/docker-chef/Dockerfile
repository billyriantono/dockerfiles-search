FROM chef/chefdk:latest

RUN apt-get update && \
  apt-get install -y --no-install-recommends python
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

RUN curl -o /tmp/get-pip.py https://bootstrap.pypa.io/get-pip.py && python /tmp/get-pip.py
RUN pip install awscli --upgrade
