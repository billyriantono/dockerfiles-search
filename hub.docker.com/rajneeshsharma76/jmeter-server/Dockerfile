# Use Rajneeshsharma76/docker-jmeter-base

FROM rajneeshsharma76/jmeterbase
MAINTAINER Rajneesh Sharma

# Ports to be exposed from the container for JMeter Slaves/Server
EXPOSE 1099 50000

# Application to run on starting the container
ENTRYPOINT $JMETER_HOME/bin/jmeter-server \
                        -Dserver.rmi.localport=50000 \
-Dserver_port=1098
