FROM ubuntu:xenial

RUN apt-get update && apt-get install -y \
    cpio \
    curl \
    dosfstools \
    gdisk \
    git \
    kpartx \
    python3-pip \
    python3.5-minimal \
    qemu-utils \
    sudo \
&& update-alternatives --install /usr/bin/python python /usr/bin/python3.5 1 \
&& cd ~ \
&& git clone https://opendev.org/openstack/diskimage-builder.git dib \
&& cd dib && pip3 install -r requirements.txt \
&& python3 setup.py install \
&& cd .. \
&& rm -rf dib/
CMD ["/bin/bash"]
