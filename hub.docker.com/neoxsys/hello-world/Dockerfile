### Example hello-world Docker file ###

FROM ubuntu:16.04
MAINTAINER Hardik 'neoXsys' Dalwadi hardik.dalwadi@gmail.com
ADD hello-world.sh /bin/
RUN apt-get update && apt-get install -y iputils-ping
ENTRYPOINT ["bash"]
CMD ["/bin/hello-world.sh"]
