FROM avkosme/centos

RUN yum -y install gcc-c++
RUN yum -y install make
RUN yum -y install wget
RUN yum -y install xz

RUN wget https://nodejs.org/dist/v10.7.0/node-v10.7.0-linux-x64.tar.xz -P /tmp
RUN unxz /tmp/node-v10.7.0-linux-x64.tar.xz
RUN tar -xvf /tmp/node-v10.7.0-linux-x64.tar -C /opt
RUN ln -s /opt/node-v10.7.0-linux-x64/bin/node /usr/bin/node
RUN ln -s /opt/node-v10.7.0-linux-x64/bin/npm /usr/bin/npm
RUN npm config set user 0
RUN npm config set unsafe-perm true
