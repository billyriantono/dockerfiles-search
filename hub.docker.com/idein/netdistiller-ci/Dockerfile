FROM ubuntu:18.04

ARG RESOLVER

#RUN apt-get update \
# && apt-get upgrade -y \
# && apt-get install -y gnupg2 dirmngr \
# && apt-get clean && rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

# https://github.com/commercialhaskell/stack/blob/master/doc/install_and_upgrade.md#ubuntu
#RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 575159689BEFB442
#RUN echo 'deb http://download.fpcomplete.com/ubuntu trusty main' | tee /etc/apt/sources.list.d/fpco.list

RUN apt-get update \
 && DEBIAN_FRONTEND=noninteractive \
    apt-get upgrade -y \
 && DEBIAN_FRONTEND=noninteractive \
    apt-get install -y --no-install-recommends \
      git ssh haskell-stack \
      valgrind libcunit1-dev doxygen lcov autoconf automake autoconf-archive libtool graphviz \
      python3 python3-pip python3-dev python3-setuptools \
      libtiff5-dev libjpeg8-dev zlib1g-dev libfreetype6-dev liblcms2-dev libwebp-dev tcl8.5-dev tk8.5-dev \
      wget sudo pandoc apt-utils locales netbase \
 && apt-get clean && rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

# default python is python3
RUN update-alternatives --install /usr/bin/python python /usr/bin/python3 1 \
 && update-alternatives --install /usr/bin/pip    pip    /usr/bin/pip3    1

RUN pip install --upgrade pip
RUN pip install Pillow
RUN pip install pypandoc
RUN pip install tensorflow
RUN pip install keras
RUN pip install h5py

# https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=782366
# RUN sed -i 's/^libdir={/libdir=\${/' /usr/lib/pkgconfig/cunit.pc \
#  && echo 'Version: 2.1.2' >> /usr/lib/pkgconfig/cunit.pc

# add idein user
RUN useradd -m idein \
 && echo idein:idein | chpasswd \
 && adduser idein sudo \
 && echo 'idein ALL=NOPASSWD: ALL' >> /etc/sudoers.d/idein

USER idein
WORKDIR /home/idein
ENV HOME /home/idein

# set locale
RUN sudo -H locale-gen en_US.UTF-8
RUN sudo update-locale LANG=en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8
ENV PATH /home/idein/.local/bin:$PATH
CMD ["/bin/bash"]

# setup stack
RUN stack upgrade
RUN mkdir -p /home/idein/.stack/global-project/
ADD stack.yaml /home/idein/.stack/global-project/stack.yaml
RUN sudo chown idein:idein /home/idein/.stack/global-project/stack.yaml
RUN sudo chmod 644 /home/idein/.stack/global-project/stack.yaml
RUN stack config set resolver ${RESOLVER}
RUN stack setup
RUN stack install \
      singletons vector data-default constraints cereal bytestring attoparsec \
      hspec QuickCheck \
      messagepack containers text \
      optparse-applicative unordered-containers mtl hashable \
      haiji
