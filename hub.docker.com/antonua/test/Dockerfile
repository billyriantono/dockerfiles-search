FROM selenium/standalone-chrome

RUN sudo apt-get update

RUN sudo apt-get install -y maven

RUN sudo apt-get -y install openjdk-8-jdk

RUN sudo mkdir -p /usr/app

WORKDIR /usr/app

COPY . /usr/app

CMD ["sudo", "mvn", "test"]
