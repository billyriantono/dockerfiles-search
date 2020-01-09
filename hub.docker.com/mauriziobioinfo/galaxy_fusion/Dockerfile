FROM bgruening/galaxy-stable

MAINTAINER Bjrn A. Grning, bjoern.gruening@gmail.com

ENV GALAXY_CONFIG_BRAND test_flavor

WORKDIR /galaxy-central

RUN add-tool-shed --url 'http://testtoolshed.g2.bx.psu.edu/' --name 'Test Tool Shed'
#RUN add-tool-shed --url 'https://toolshed.g2.bx.psu.edu/' --name 'mytoolsheed'
# Install Visualisation
RUN install-biojs msa

# Adding the tool definitions to the container
ADD my_test_list.yml $GALAXY_ROOT/my_test_list.yml

# Install my_tools_list
RUN install-tools $GALAXY_ROOT/my_test_list.yml

# Mark folders as imported from the host.
VOLUME ["/export/", "/data/", "/var/lib/docker"]

# Expose port 80 (webserver), 21 (FTP server), 8800 (Proxy)
EXPOSE :80
EXPOSE :21
EXPOSE :8800

# Autostart script that is invoked during container start
CMD ["/usr/bin/startup"]
