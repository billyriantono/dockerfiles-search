FROM library/ubuntu

RUN apt-get update && \
    apt-get -y install wget && \
    apt-get -y install xz-utils && \
    apt-get -y install curl gnupg

RUN curl -sL https://deb.nodesource.com/setup_11.x  | bash -

RUN apt-get -y install nodejs && \
    cd ~ 
RUN npm install sfdx-cli --production --global

CMD ["sfdx", "--verison"]

RUN apt-get -y install git 
    
RUN apt-get install -y openjdk-8-jdk && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/* && \
	rm -rf /var/cache/oracle-jdk8-installer

RUN apt-get install -y ca-certificates-java && \
	apt-get clean && \
	update-ca-certificates -f && \
	rm -rf /var/lib/apt/lists/* && \
	rm -rf /var/cache/oracle-jdk8-installer

RUN apt-get update && \
	apt-get -y install ant

RUN apt-get update && \
	apt-get -y install ant-contrib

RUN apt-get -y install jq && \
	apt-get update 

RUN apt-get -y install software-properties-common 



RUN apt-get update && \
	apt-get -y install python3.6 && \
	python3 --version;



ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64/
RUN export JAVA_HOME