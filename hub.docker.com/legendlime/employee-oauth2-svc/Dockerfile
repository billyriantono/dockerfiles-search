FROM openjdk:12-jdk-alpine
RUN apk update && apk upgrade && apk add netcat-openbsd
RUN mkdir -p /usr/local/employeeservice
ADD EmployeeService-OAuth2-0.1-DRAFT.jar /usr/local/employeeservice/
ADD run.sh run.sh
RUN chmod +x run.sh
CMD ./run.sh
