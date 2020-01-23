FROM cptactionhank/atlassian-jira:latest

MAINTAINER Wojciech Wójcik <wojtaswojcik@gmail.com>

USER root

RUN wget -o ${JIRA_INSTALL}/lib/postgresql-9.4-1208.jar https://jdbc.postgresql.org/download/postgresql-9.4.1208.jar

USER daemon:daemon