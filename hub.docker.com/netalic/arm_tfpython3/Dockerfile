FROM resin/rpi-raspbian:latest
MAINTAINER Merdan <@merdan>

# Set the variables
ENV DEBIAN_FRONTEND noninteractive
ENV PHTHON_VERSION 3.5.2

WORKDIR /root

# Install packages necessary for compiling python
#RUN apt-get update --fix-missing
#RUN apt-get -y upgrade
    
RUN apt-get install -y build-essential libncursesw5-dev libgdbm-dev libc6-dev zlib1g-dev libsqlite3-dev tk-dev libssl-dev openssl

# Download and compile python
RUN apt-get install -y ca-certificates
ADD "https://www.python.org/ftp/python/${PHTHON_VERSION}/Python-${PHTHON_VERSION}.tgz" /root/Python-${PHTHON_VERSION}.tgz
RUN tar zxvf "Python-${PHTHON_VERSION}.tgz"; \
        cd Python-${PHTHON_VERSION}; \
        ./configure; \
        make; \
        make install; \
        cd ..; \
        rm -rf "./Python-${PHTHON_VERSION}" ;\
        rm "./Python-${PHTHON_VERSION}.tgz"

# Update pip and install jupyter
RUN apt-get install -y libncurses5-dev
RUN pip3 install --upgrade pip
RUN pip3 install readline jupyter

RUN apt-get update --fix-missing ;\
    apt-get install -y wget bzip2 ca-certificates libglib2.0-0 libxext6 libsm6 libxrender1 git mercurial subversion

RUN wget https://github.com/samjabrahams/tensorflow-on-raspberry-pi/raw/master/bin/tensorflow-0.10.0-py3-none-any.whl
RUN pip3 install tensorflow-0.10.0-py3-none-any.whl

# Configure jupyter
RUN jupyter notebook --generate-config
RUN mkdir notebooks
RUN sed -i "/c.NotebookApp.open_browser/c c.NotebookApp.open_browser = False" /root/.jupyter/jupyter_notebook_config.py ;\
    sed -i "/c.NotebookApp.ip/c c.NotebookApp.ip = '*'" /root/.jupyter/jupyter_notebook_config.py ;\
    sed -i "/c.NotebookApp.notebook_dir/c c.NotebookApp.notebook_dir = '/root/notebooks'" /root/.jupyter/jupyter_notebook_config.py

VOLUME /root/notebooks

# Add Tini. Tini operates as a process subreaper for jupyter. This prevents kernel crashes.
ENV TINI_VERSION 0.9.0
ENV CFLAGS="-DPR_SET_CHILD_SUBREAPER=36 -DPR_GET_CHILD_SUBREAPER=37"

ADD https://github.com/krallin/tini/archive/v${TINI_VERSION}.tar.gz /root/v${TINI_VERSION}.tar.gz
RUN apt-get install -y cmake
RUN tar zxvf v${TINI_VERSION}.tar.gz ;\
        cd tini-${TINI_VERSION} ;\
        cmake . ;\
        make ;\
        cp tini /usr/bin/. ;\
        cd .. ;\
        rm -rf "./tini-${TINI_VERSION}" ;\
        rm "./v${TINI_VERSION}.tar.gz"

ENTRYPOINT ["/usr/bin/tini", "--"]

EXPOSE 8888

CMD ["jupyter", "notebook"]
