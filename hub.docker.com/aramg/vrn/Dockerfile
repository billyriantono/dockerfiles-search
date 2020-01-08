FROM aramg/vrn-dependencies
MAINTAINER Aram Grigoryan <aram.grigoryan@gmail.com>

# Clone vrn repo
WORKDIR /workspace
RUN chmod -R a+w /workspace
RUN git clone --recursive https://github.com/AaronJackson/vrn.git
WORKDIR /workspace/vrn
#RUN ./download.sh
#RUN ./run.sh