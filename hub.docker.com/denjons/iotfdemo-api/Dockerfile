FROM maven:3.5


# Install necessary packages
COPY . /src

RUN mkdir app && cd /src && mvn clean package && cd ./target && mv iotf-demo-api-swarm.jar /app

ENV HOST 0.0.0.0
ENV PORT_OFFSET 0

EXPOSE 8080

#-Dswarm.bind.address=$HOST -Dswarm.port.offset=$PORT_OFFSET
CMD cd /app && java -jar iotf-demo-api-swarm.jar -Dswarm.bind.address=$HOST -Dswarm.port.offset=$PORT_OFFSET
