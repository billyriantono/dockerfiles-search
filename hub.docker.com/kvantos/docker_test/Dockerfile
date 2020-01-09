FROM openjdk
LABEL Author="Skviato" Company="Slice"

RUN echo "Copy jar file"
COPY Task9 /opt/Task9
WORKDIR /opt/Task9

RUN echo "Building file"
RUN javac Sample.java

#ENTRYPOINT ["/usr/bin/java /opt/Task9/Sample"]
CMD java Sample
#ENTRYPOINT "/usr/bin/bash"

#ARG MESSAGE_ARG='Building message... over arg'

ENV message $MESSAGE_ARG
RUN echo $message

