FROM thepauleh/jenkins-slave

RUN apt-get update && apt-get install -y -q \
    python-setuptools \
      python-pip \
      python-dev \
      libpq-dev \
      libxml2-dev \
      libjpeg-dev \
      libxslt1-dev \
      python-imaging \
      libxml2-utils \
    && rm -rf /var/lib/apt/lists/*

RUN pip install fabric
RUN pip install -I pillow
RUN pip install virtualenv
RUN pip install virtualenvwrapper
