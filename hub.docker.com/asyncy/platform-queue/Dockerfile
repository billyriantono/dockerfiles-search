FROM	debian:stretch

RUN	apt-get update

# Install OpenJDK.
RUN mkdir -p /usr/share/man/man1 && \
    (echo "deb http://http.debian.net/debian stretch-backports main" > /etc/apt/sources.list.d/backports.list) && \
    apt-get update -y && \
    apt-get install -t stretch-backports openjdk-8-jdk-headless -y

RUN	apt-get -y install curl unzip maven

# Compile and build our app.
RUN     mkdir /app
ADD     src /app/src
COPY    pom.xml /app
RUN     cd /app && mvn package

EXPOSE  8080

CMD     ["java", "-jar", "/app/target/platform-queue-jar-with-dependencies.jar"]

