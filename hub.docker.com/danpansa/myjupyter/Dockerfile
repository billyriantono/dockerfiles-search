# danpansa/mujupyter:0.21
#
# jupyter on ubuntu-debootstrap:14.04.3
# Python3(anaconda) & Julia were installed.

FROM ubuntu-debootstrap:14.04.3
MAINTAINER Osamu KOMAGATA <cat.rocky@gmail.com>

# export DEBIAN_FRONTEND="noninteractive"
ENV DEBIAN_FRONTEND noninteractive

# locale setting
RUN locale-gen en_US.UTF-8
RUN locale-gen ja_JP.UTF-8

# timezone setting
RUN echo "Asia/Tokyo" > /etc/timezone
RUN dpkg-reconfigure -f noninteractive tzdata

RUN apt-get update
RUN apt-get -y install software-properties-common
RUN apt-get -y install apt-utils
RUN add-apt-repository ppa:staticfloat/juliareleases
RUN add-apt-repository ppa:staticfloat/julia-deps
RUN apt-get update

RUN apt-get -y install language-pack-ja

RUN apt-get -y install ssh curl build-essential vim zsh wget net-tools libnettle4
RUN apt-get -y install gcc libhdf5-dev
RUN chsh -s /usr/bin/zsh

RUN apt-get -y install julia

RUN cd ~
RUN mkdir ~/anaconda
RUN cd ~/anaconda
RUN wget https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.4.1-Linux-x86_64.sh
RUN bash Anaconda3-2.4.1-Linux-x86_64.sh -b
ENV PATH /root/anaconda3/bin:~:$PATH

RUN conda install -y jupyter
RUN conda install -y pystan
RUN pip install chainer
EXPOSE 8888

RUN touch /root/install_Ijulia.jl
RUN echo 'Pkg.add("PyPlot")' >> /root/install_Ijulia.jl
RUN echo 'Pkg.add("Gadfly")' >> /root/install_Ijulia.jl
RUN echo 'Pkg.add("IJulia")' >> /root/install_Ijulia.jl
RUN echo 'Pkg.build("IJulia")' >> /root/install_Ijulia.jl
RUN echo 'Pkg.update()' >> /root/install_Ijulia.jl
RUN julia /root/install_Ijulia.jl
RUN rm /root/install_Ijulia.jl

RUN touch /root/myjupyter.sh
RUN echo '#!/bin/sh' >> /root/myjupyter.sh
RUN echo 'jupyter notebook --no-browser --ip=* /notebooks &' >> /root/myjupyter.sh
RUN chmod u+x /root/myjupyter.sh

RUN mkdir /notebooks
VOLUME /notebooks
WORKDIR /notebooks
