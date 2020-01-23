FROM       cjvaz/ubuntu
MAINTAINER Carlos José Vaz <carlosjvaz@gmail.com>

# install python
RUN apt-get -y -qq update
RUN apt-get install -y -qq --no-install-recommends \
                     python python-dev python-setuptools \
                     python-pip libpq-dev

# install virtualenv
RUN pip install virtualenv virtualenvwrapper

# clean
RUN apt-get autoremove && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*  /var/cache/apt/*