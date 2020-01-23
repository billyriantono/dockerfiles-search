FROM ubuntu:18.04
MAINTAINER Andrea Censi

ENV refreshed_ON=20190201
RUN apt-get update

ARG DEBIAN_FRONTEND=noninteractive
#RUN apt-get install -y dialog apt-utils

#RUN apt-get install -y \
#    apt-transport-https

#RUN apt-get update
# todo:
#    pdftk \
#    python-imaging \

RUN apt-get install -y \
    git \
    git-lfs \
    git-extras \
    ssh \
    bibtex2html \
    libxml2-dev \
    libxslt1-dev \
    libffi6 \
    libffi-dev \
    libxml2-dev \
    libxslt1-dev \
    bibtex2html \
    build-essential \
    graphviz \
    idle \
    virtualenv \
    python-pmw \
    python-yaml \
    python-dev \
    python-setproctitle \
    python-psutil \
    python-tk \
    python-scipy \
    python-frozendict \
    python-termcolor \
    python-setproctitle \
    python-psutil\
    python-mysqldb\
    byobu \
    atop \
    htop \
    imagemagick \
    graphviz \
    ghostscript \
    git-lfs \
    ntpdate  \
    libatlas-base-dev \
    vim\
    apt-file\
    iftop\
    node-less\
    libcurl4\
    libgif7\
    rsync\
    zsh\
    npm\
    curl\
    python3-pip\
    ncdu


RUN wget https://www.princexml.com/download/prince_12.4-1_ubuntu18.04_amd64.deb && \
    dpkg -i prince_12.4-1_ubuntu18.04_amd64.deb
RUN rm prince_12.4-1_ubuntu18.04_amd64.deb


RUN mkdir /project

WORKDIR /project
RUN npm install -g mathjax-node-page@3.0.1 less@3.9.0 stylelint


RUN python --version
RUN python3 --version
# for linkchecker
RUN apt-get install -y python-pip
RUN git clone https://github.com/AndreaCensi/linkchecker.git
# note: this must use python2 and needs the apt package python-pip as well (setuptools)
RUN cd linkchecker && python2 setup.py install
RUN  linkchecker --version

COPY docker/fix.py /project/fix.py
RUN /project/fix.py



COPY requirements.txt /requirements.txt
RUN pip3 install -r /requirements.txt

COPY requirements-own.txt /requirements-own.txt
RUN pip3 install -r /requirements-own.txt

# make python3 default
RUN update-alternatives --install /usr/bin/python python /usr/bin/python3 10



RUN curl -L -o reveal-3.6.0.zip https://github.com/hakimel/reveal.js/archive/3.6.0.zip
RUN echo "534378be63e218338e46430a106e2def  /project/reveal-3.6.0.zip" > md5-checks.txt
RUN md5sum -c md5-checks.txt


ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8
RUN python3 -c "print('\u25f6')"


RUN apt-get clean




RUN mkdir /project/mcdp
COPY Makefile.cython /project/mcdp
COPY Makefile* /project/mcdp/
COPY setup.py /project/mcdp
COPY src /project/mcdp/src
# XXX: some are not empty
# RUN find  /project/mcdp/src -type d -name out\* -delete
COPY misc /project/mcdp/misc

RUN cp -R /project/mcdp/misc/fonts /usr/share/fonts/my-fonts
RUN fc-cache -f -v


# Delete files generated from outside
RUN find mcdp/src -name '*.so' -delete
RUN find mcdp/src -name '*.c' -delete

# TODO: reactivate this

# RUN . deploy/bin/activate && cd mcdp && make -f Makefile.cython -j3
# RUN . deploy/bin/activate && cd mcdp && make -f Makefile.cython delete-python-files

#   --no-deps should avoid downloading dependencies
RUN  cd /project/mcdp && python3 setup.py develop --no-deps

ENV DISABLE_CONTRACTS=1
RUN mcdp-render-manual --help

COPY docker/entrypoint.sh /project/entrypoint.sh
RUN chmod +x /project/entrypoint.sh

COPY docker/copy_dir.sh /project/copy_dir.sh
RUN chmod +x /project/copy_dir.sh


RUN chmod 0777 /project

COPY books/run-book-native.sh /project/run-book-native.sh


ENTRYPOINT ["/project/entrypoint.sh"]
