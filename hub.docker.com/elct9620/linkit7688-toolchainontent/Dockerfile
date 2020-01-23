FROM mozilla/sbt

ENV repo_name communication_backend
ENV repo_link https://github.com/elasticbots/${repo_name}
ENV SBT_VERSION 1.3.0

ENV ELB__DB_SERVER_NAME=communication_db
ENV ELB__DB_PORT_NUMBER=65000
ENV ELB__DB_NAME=elb_communication
ENV ELB__DB_USER=postgres
ENV ELB__DB_PASSWORD=postgres
ENV ELB__COMMUNICATION_BACKEND_URL=management_backend
ENV ELB__COMMUNICATION_BACKEND_PORT=8080
ENV ELB__AUTH_ENDPOINT=authenticate

ADD . $ELB__DB_SERVER_NAME
ADD . $ELB__DB_PORT_NUMBER
ADD . $ELB__DB_NAME
ADD . $ELB__DB_USER
ADD . $ELB__DB_PASSWORD
ADD . $ELB__COMMUNICATION_BACKEND_URL
ADD . $ELB__COMMUNICATION_BACKEND_PORT
ADD . $ELB__AUTH_ENDPOINT

EXPOSE 9000

COPY scala /local/server
WORKDIR /local/server

RUN sbt clean stage

CMD ["target/universal/stage/bin/comunications"]

