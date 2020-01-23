from bryandollery/devbox

run curl -sSLO https://github.com/ForgeRock/openam-community-edition/releases/download/ce%2F11.0.3/OpenAM-Community-Edition-11.0.3.war && \
    mkdir -p /war && \
    mv OpenAM-Community-Edition-11.0.3.war /war/
run curl -sSLO http://www-eu.apache.org/dist/tomcat/tomcat-8/v8.5.31/bin/apache-tomcat-8.5.31.tar.gz && \
    mkdir -p /tomcat && \
    tar -xzf apache-tomcat-8.5.31.tar.gz -C /tomcat --strip-components 1 && \
    rm /apache-tomcat-8.5.31.tar.gz && \
    echo "export PATH=$PATH:/tomcat/bin" >> /root/.bashrc
run mv /war/OpenAM-Community-Edition-11.0.3.war /tomcat/webapps/openam.war

entrypoint ["/bin/bash", "/tomcat/bin/catalina.sh", "run"]

expose 8080
