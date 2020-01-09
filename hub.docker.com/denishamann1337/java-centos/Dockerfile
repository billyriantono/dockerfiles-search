FROM centos:7

RUN yum update -y && \
    yum install -y wget
RUN wget https://download.java.net/java/GA/jdk13/5b8a42f3905b406298b72d750b6919f6/33/GPL/openjdk-13_linux-x64_bin.tar.gz
RUN tar xzf openjdk-13_linux-x64_bin.tar.gz -C /usr/local
RUN cd /usr/local/jdk-13
RUN alternatives --install /usr/bin/java java /usr/local/jdk-13/bin/java 2
RUN alternatives --set java /usr/local/jdk-13/bin/java
RUN yum install -y freetype
RUN yum install -y urw-fonts
RUN yum install -y iproute
RUN yum install -y openssl098e
RUN yum install -y unzip
RUN yum clean all
RUN ln -s /usr/lib64/libexpat.so.1 /usr/lib64/libexpat.so.0

# Set environment variables.
ENV HOME /root

# Define working directory.
WORKDIR /root

# Define default command.
CMD ["bash"]
