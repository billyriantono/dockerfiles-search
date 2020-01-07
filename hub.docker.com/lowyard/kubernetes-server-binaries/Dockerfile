FROM centos
WORKDIR /opt
ENV HASH 28b2703c95894ab0565e372517c4a4b2c33d1be3d778fae384a6ab52c06cea7dd7ec80060dbdba17c8ab23bbedcde751cccee7657eba254f7d322cf7c4afc701
RUN curl -L -O https://dl.k8s.io/v1.17.0/kubernetes-server-linux-amd64.tar.gz 
RUN CURRENT=$(cat kubernetes-server-linux-amd64.tar.gz | sha512sum | tr -d ' -'); echo ${CURRENT}; [[ ${CURRENT} == ${HASH} ]] || echo failed; [[ ${CURRENT} == ${HASH} ]] && echo successed 
