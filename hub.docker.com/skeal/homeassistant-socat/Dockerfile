FROM "openhab/openhab:latest"
LABEL maintainer="skeal"

RUN mkdir /runwatch
COPY runwatch/run.sh /runwatch/run.sh

# Install socat
RUN apt update
RUN apt install apt-utils -y
RUN apt install socat -y

# Monitor socat
COPY runwatch/100.socat-zwave.enabled.sh /runwatch/100.socat-zwave.enabled.sh

# clear apt stuff

CMD [ "bash","/runwatch/run.sh" ]
