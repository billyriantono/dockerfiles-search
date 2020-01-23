FROM nvidia/opencl

RUN apt-get update
RUN apt-get install git cmake g++ curl wget -y

WORKDIR /root

RUN wget -O boost_1_66_0.tar.gz http://sourceforge.net/projects/boost/files/boost/1.66.0/boost_1_66_0.tar.gz/download   
RUN tar xzvf boost_1_66_0.tar.gz   

WORKDIR /root/boost_1_66_0

RUN ls
RUN ./bootstrap.sh   
RUN ./b2 --prefix=../[boost] link=static install   
RUN cd ..

RUN git clone --recursive https://github.com/clemahieu/raiblocks.git /root/rai_build   

WORKDIR /root/rai_build

RUN ls

RUN cmake -DBOOST_ROOT=../[boost]/ -G "Unix Makefiles"   
RUN make rai_node   

RUN mkdir /root/data

CMD /root/rai_build/rai_node --daemon --data_path /root/data
