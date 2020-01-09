FROM tomitribe/adminlab1:complete

ENV PATH /usr/local/apache-maven-3.2.5/bin:$PATH

RUN cd ~ && \
    sudo apt-get -y install git && \
    sudo wget -q http://mirrors.fe.up.pt/pub/apache/maven/maven-3/3.2.5/binaries/apache-maven-3.2.5-bin.tar.gz && \
    sudo tar -zxf apache-maven-3.2.5-bin.tar.gz -C /usr/local/ && \
    sudo rm -rf apache-maven-3.2.5-bin.tar.gz && \
    git clone https://github.com/tomitribe/agoncal-application-petstore-ee6.git petstore && \
    cd petstore && \
    git checkout adminlab2 && \
    mvn clean install -Dmaven.test.skip=true
