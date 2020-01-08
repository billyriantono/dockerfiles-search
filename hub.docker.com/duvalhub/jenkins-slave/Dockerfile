FROM docker AS docker-client
FROM mikefarah/yq AS yq-client
FROM 'jenkins/slave'
COPY --from=docker-client /usr/local/bin/docker /usr/bin/docker
COPY --from=yq-client /usr/bin/yq /usr/bin/yq
#USER root
#COPY yq /usr/bin/yq
#RUN curl https://github.com/mikefarah/yq/releases/download/2.4.1/yq_linux_amd64 > 
#RUN apt-get update \
#&& apt-get install -y software-properties-common \
#&& add-apt-repository ppa:rmescandon/yq \
#&& apt-get update \
#&& apt-get install -y yq
#COPY --from=docker-client /usr/lib/x86_64-linux-gnu/libapparmor.so.1 /usr/lib/x86_64-linux-gnu/libapparmor.so.1
#USER jenkins
#COPY --from=docker-client /lib/x86_64-linux-gnu/libdevmapper.so.1.02.1 /lib/x86_64-linux-gnu/libdevmapper.so.1.02.1