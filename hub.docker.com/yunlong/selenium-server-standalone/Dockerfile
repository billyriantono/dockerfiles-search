FROM java

RUN apt-get update && apt-get upgrade -y

RUN cd /opt && wget http://selenium-release.storage.googleapis.com/3.3/selenium-server-standalone-3.3.1.jar
RUN wget https://chromedriver.storage.googleapis.com/2.9/chromedriver_linux64.zip && unzip chromedriver_linux64.zip -d /usr/bin

EXPOSE 4444

ENTRYPOINT  ["/bin/bash", "-c", "java -jar /opt/selenium-server-standalone-3.3.1.jar"]