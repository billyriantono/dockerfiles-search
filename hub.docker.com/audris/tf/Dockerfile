FROM ubuntu:14.04

MAINTAINER Audris Mockus <audris@utk.edu>
MAINTAINER Based on https://github.com/tensorflow/tensorflow/blob/master/tensorflow/tools/docker/Dockerfile

RUN apt-get update && apt-get install -y \
        curl \
        libfreetype6-dev \
        libpng12-dev \
        libzmq3-dev \
        pkg-config \
        python-numpy \
        python-pip \
        python-scipy \
		vim \
		sssd \
		openssh-server \
		openssh-client \
		libpam-sss \
		sssd-tools \
        && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN curl -O https://bootstrap.pypa.io/get-pip.py && \
    python get-pip.py && \
    rm get-pip.py

RUN pip --no-cache-dir install \
        ipykernel \
        jupyter \
        matplotlib \
		scikit-learn \
        && \
    python -m ipykernel.kernelspec

# Install TensorFlow CPU version.
ENV TENSORFLOW_VERSION 0.7.1
RUN pip --no-cache-dir install \
    http://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-${TENSORFLOW_VERSION}-cp27-none-linux_x86_64.whl

#install ldap authentication to use utk's ldap
COPY eecsCA_v3.crt /etc/ssl/
COPY sssd.conf /etc/sssd/
COPY common* /etc/pam.d/
RUN chmod 0600 /etc/sssd/sssd.conf /etc/pam.d/common* 
RUN mkdir -p /var/run/sshd 
RUN chmod 0755 /var/run/sshd


# Set up our notebook config.
COPY jupyter_notebook_config.py /root/.jupyter/
COPY notebooks /notebooks
COPY run_jupyter.sh /

# TensorBoard
EXPOSE 6006
# IPython
EXPOSE 8888

WORKDIR "/notebooks"

#CMD ["/run_jupyter.sh"]
