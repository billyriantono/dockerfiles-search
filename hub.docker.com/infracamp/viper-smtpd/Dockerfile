FROM infracamp/kickstart-flavor-gaia:testing

ENV DEV_CONTAINER_NAME="viper-smtpd"

ADD / /opt
RUN ["bash", "-c",  "chown -R user /opt"]
RUN ["/kickstart/flavorkit/scripts/start.sh", "build"]

ENTRYPOINT ["/kickstart/flavorkit/scripts/start.sh", "standalone"]