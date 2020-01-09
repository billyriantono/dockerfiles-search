FROM maven:3.5


# Install necessary packages
COPY . /src

RUN cd /src && mvn clean package && cd ./target && mv test3-swarm.jar /app

EXPOSE 8080

CMD cd /app && java -jar test3-swarm.jar
