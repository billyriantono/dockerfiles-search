FROM openjdk:12-jdk-oraclelinux7

WORKDIR /root

#Installing required packages
RUN yum update -y && yum install -y wget xz

#Installing NodeJs
RUN wget https://nodejs.org/dist/v12.2.0/node-v12.2.0-linux-x64.tar.xz
RUN unxz node-v12.2.0-linux-x64.tar.xz && tar --strip-components 1 -xvf node-v12.2.0-linux-x64.tar -C /usr/local
RUN npm i -g yarn

#Installing Azure CLI
RUN rpm --import https://packages.microsoft.com/keys/microsoft.asc
RUN sh -c 'echo -e "[azure-cli]\nname=Azure CLI\nbaseurl=https://packages.microsoft.com/yumrepos/azure-cli\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/azure-cli.repo'
RUN yum install -y azure-cli

#Installing maven
RUN wget https://www-us.apache.org/dist/maven/maven-3/3.6.1/binaries/apache-maven-3.6.1-bin.tar.gz
RUN tar xvf apache-maven-3.6.1-bin.tar.gz
RUN mv apache-maven-3.6.1 /usr/local/apache-maven

#Setting env vars
ENV M2_HOME=/usr/local/apache-maven
ENV M2=$M2_HOME/bin
ENV PATH $JAVA_HOME/bin:$M2_HOME/bin:$M2:$PATH

CMD bash