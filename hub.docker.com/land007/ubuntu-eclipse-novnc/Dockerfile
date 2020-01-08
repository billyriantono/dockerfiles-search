FROM land007/ubuntu-unity-novnc:latest

MAINTAINER Yiqiu Jia <yiqiujia@hotmail.com>

# Install Java.
RUN \
  echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
  add-apt-repository -y ppa:webupd8team/java && \
  apt-get update && \
  apt-get install -y oracle-java8-installer && \
  rm -rf /var/lib/apt/lists/* && \
  rm -rf /var/cache/oracle-jdk8-installer

# Define commonly used JAVA_HOME variable
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle
ENV CLASSPATH .:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
ENV PATH $PATH:$JAVA_HOME/bin
RUN echo 'export JAVA_HOME=/usr/lib/jvm/java-8-oracle' >> /etc/profile && echo 'export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar' >> /etc/profile && echo 'export PATH=$PATH:$JAVA_HOME/bin' >> /etc/profile
# Eclipse
RUN cd /tmp && wget http://mirror.rise.ph/eclipse//technology/epp/downloads/release/photon/R/eclipse-jee-photon-R-linux-gtk-x86_64.tar.gz && tar -zxvf eclipse-jee-photon-R-linux-gtk-x86_64.tar.gz -C /usr/local/ && rm -f eclipse-jee-photon-R-linux-gtk-x86_64.tar.gz
ADD eclipse.desktop /usr/share/applications/eclipse.desktop

# eclipse
RUN mv /usr/local/eclipse /usr/local/eclipse_
VOLUME ["/usr/local/eclipse"]
 
# Define working directory.
RUN mkdir /eclipse-workspace
#ADD eclipse-workspace /eclipse-workspace
WORKDIR /eclipse-workspace
RUN ln -s /eclipse-workspace ~/
RUN ln -s /eclipse-workspace /home/land007
RUN mv /eclipse-workspace /eclipse-workspace_
VOLUME ["/eclipse-workspace"]

#CMD ["/bin/bash", "/home/ubuntu/startup.sh"]
CMD /check.sh /home/ubuntu/.config/google-chrome/Default ; /check.sh /eclipse-workspace ; /check.sh /usr/local/eclipse ; /etc/init.d/ssh start ; nohup /home/ubuntu/startup.sh > /tmp/startup.out 2>&1 & sleep 2 ; cat /home/ubuntu/password.txt ; bash

#sudo docker exec $CONTAINER_ID cat /home/ubuntu/password.txt
#docker pull land007/ubuntu-eclispe-novnc ; docker stop ubuntu-eclispe-novnc ; docker rm ubuntu-eclispe-novnc ; docker run -it -p 5901:5901 -p 6080:6080 -p 4040:4040 --privileged --name ubuntu-eclispe-novnc land007/ubuntu-eclispe-novnc:latest
#docker pull land007/ubuntu-eclispe-novnc ; docker stop ubuntu-eclispe-novnc ; docker rm ubuntu-eclispe-novnc ; docker run -it -v ~/docker/eclipse-workspace:/eclipse-workspace -v ~/docker/eclipse:/usr/local/eclipse -p 5901:5901 -p 6080:6080 -p 4040:4040 --privileged --name ubuntu-eclispe-novnc land007/ubuntu-eclispe-novnc:latest
#docker pull land007/ubuntu-eclispe-novnc ; docker stop ubuntu-eclispe-novnc ; docker rm ubuntu-eclispe-novnc ; docker run -it -v ~/docker/chrome_default:/home/ubuntu/.config/google-chrome/Default -v ~/docker/eclipse-workspace:/eclipse-workspace -v ~/docker/eclipse:/usr/local/eclipse -p 5901:5901 -p 6080:6080 -p 4040:4040 -p 2020:20022 --privileged --name ubuntu-eclispe-novnc land007/ubuntu-eclispe-novnc:latest
