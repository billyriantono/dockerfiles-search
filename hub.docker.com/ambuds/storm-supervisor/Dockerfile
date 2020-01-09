FROM ambuds/storm-base
MAINTAINER ambuds

EXPOSE 6700
EXPOSE 8000

# Set configuration script as executable
ADD storm-supervisor.sh /opt/
RUN chmod +x /opt/*.sh

CMD /opt/storm-supervisor.sh

