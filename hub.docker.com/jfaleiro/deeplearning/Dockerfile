# deeplearning - deep learning in a box, an image carrying all the basic tools 
# of deeplearning
# 
# Copyright (C) 2018 Jorge M. Faleiro Jr.
#  
# This program is free software: you can redistribute it and/or modify
# it under the terms of the GNU Affero General Public License as published
# by the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.
#  
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU Affero General Public License for more details.
#  
# You should have received a copy of the GNU Affero General Public License
# along with this program. If not, see <http://www.gnu.org/licenses/>.
#
FROM ubuntu:16.04
LABEL maintainer="j@falei.ro"
ENV PATH /opt/conda/bin:$PATH
# tools
RUN apt-get update
RUN apt-get -y -qq install curl bzip2 iproute2
# anaconda
RUN curl -O https://repo.continuum.io/archive/Anaconda3-5.0.1-Linux-x86_64.sh
RUN bash Anaconda3-5.0.1-Linux-x86_64.sh -b -p /opt/conda
RUN rm -f Anaconda3-5.0.1-Linux-x86_64.sh
RUN ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh 
RUN conda install -c conda-forge tensorflow
RUN conda install -c conda-forge tensorboard 
RUN mkdir -p /work/notebooks
RUN mkdir -p /root/images
RUN mkdir -p /work/deeplogs
EXPOSE 8888
EXPOSE 6006
COPY ./scripts /usr/local/bin
COPY ./work/notebooks/*.ipynb /root/images/
# start 
CMD start_container.sh