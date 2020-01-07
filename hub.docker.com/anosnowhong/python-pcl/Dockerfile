FROM ubuntu:14.04

RUN apt-get update && apt-get install -y software-properties-common \
&& add-apt-repository ppa:v-launchpad-jochen-sprickerhof-de/pcl -y 

RUN apt-get update && apt-get install -y libpcl-all 

RUN apt-get install -y python-pip \
python-dev \
git \
&& pip install cython==0.25.2 \
&& pip install numpy

RUN cd /root \
&& git clone https://github.com/strawlab/python-pcl \
&& cd python-pcl 

COPY setup.py /root/python-pcl/

#install pypcap 
#RUN apt-get install -y python-pyrex libpcap0.8 libpcap0.8-dev \
#&& cd /root \
#&& git clone https://github.com/pynetwork/pypcap \
#&& cd pypcap 
RUN apt-get install -y libpcap0.8 libpcap0.8-dev \
&& pip install pypcap \
&& cd /root/python-pcl \ 

