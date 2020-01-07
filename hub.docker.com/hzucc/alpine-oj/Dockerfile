FROM frolvlad/alpine-glibc
ADD compile.cpp /
ADD runCode.cpp /
#get java8
RUN wget --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u141-b15/336fa29ff2bb4ef291e347e091f7f4a7/jdk-8u141-linux-x64.tar.gz" \
&& tar -xzf jdk-8u141-linux-x64.tar.gz \
&& mv jdk1.8.0_141 /usr/local/jdk1.8.0_141 \
&& rm jdk-8u141-linux-x64.tar.gz \
#get go
&& wget https://dl.google.com/go/go1.13.3.linux-amd64.tar.gz \
&& tar -C /usr/local -xzf go1.13.3.linux-amd64.tar.gz \
&& rm go1.13.3.linux-amd64.tar.gz \
#get g++
&& apk add --no-cache g++ \
#get python3
&& apk add python3 \

#delete compile and runCode
&& g++ compile.cpp -o compile -O3 \
&& g++ runCode.cpp -o runCode -O3 \
&& rm compile.cpp \
&& rm runCode.cpp

ENV JAVA_HOME=/usr/local/jdk1.8.0_141
ENV JRE_HOME=${JAVA_HOME}/jre
ENV CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
ENV PATH=${PATH}:${JAVA_HOME}/bin:/usr/local/go/bin



