FROM ggwhite/centos-java:latest

MAINTAINER ggwhite <ggw.chang@gmail.com>

### Actions
# 下載 maven
# 解壓縮 maven
# 移除 tar 檔

RUN wget "http://apache.stu.edu.tw/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz" && \ 
	tar xzvf apache-maven-3.3.9-bin.tar.gz -C /opt/ && \ 
	rm -f ./apache-maven-3.3.9-bin.tar.gz && \
	mkdir /opt/maven-work

# Set environment variables.
ENV HOME /opt/maven-work
ENV PATH /opt/apache-maven-3.3.9/bin:${PATH}

# Define working directory.
WORKDIR /opt/maven-work

# Define Volume
VOLUME /opt/maven-work

# Define default command.
CMD ["/bin/bash"]