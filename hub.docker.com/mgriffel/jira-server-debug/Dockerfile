FROM cptactionhank/atlassian-jira:7.6.3

LABEL Description="This image is used to start Atlassian JIRA in debug mode" Vendor="mgriffel" Version=7.6.3-1

MAINTAINER mgriffel <michael.griffel@gmail.com>

ENV JPDA_ADDRESS="5000"
ENV JPDA_TRANSPORT="dt_socket"

USER daemon:daemon

# Run Atlassian JIRA as a foreground process by default.
CMD ["/opt/atlassian/jira/bin/catalina.sh", "jpda", "run"]
