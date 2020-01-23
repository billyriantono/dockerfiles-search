FROM tensorflow/tensorflow:1.11.0-devel-gpu-py3
MAINTAINER Alex Yang <aleozlx@gmail.com>

# System dependencies
RUN apt-get -y update && apt-get install -y build-essential gfortran libblas-dev liblapack-dev libatlas-base-dev libssl-dev vim wget python3-dev python3-pip python3-tk

# VSCode
RUN curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
RUN install -o root -g root -m 644 microsoft.gpg /etc/apt/trusted.gpg.d/
RUN sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'
RUN apt-get -y install apt-transport-https
RUN apt-get -y update
RUN apt-get -y install libasound2 code

# Python packages
RUN pip3 install --upgrade pip
RUN BLAS=/usr/lib/libblas/libblas.so LAPACK=/usr/lib/lapack/liblapack.so pip3 --no-cache-dir install numpy>=1.15.0 scipy
#RUN pip3 install numba
COPY requirements.txt /requirements.txt
RUN pip3 --no-cache-dir install -r /requirements.txt

RUN apt-get install sudo gosu
COPY bashrc.sh /bin/tkstack-bashrc.sh
COPY start.sh /bin/tkstack-start.sh

# Bugfix
COPY util.patch /tmp/util.patch
RUN patch /usr/lib/python3.5/importlib/util.py /tmp/util.patch

ENTRYPOINT ["/bin/tkstack-start.sh"] 
