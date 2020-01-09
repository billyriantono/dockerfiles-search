#FROM pingcr.azurecr.io/sliq/jmbase
FROM yangpingcd/jmbase

# set rmi.localport and disalbe ssl
COPY rmi_keystore.jks ${JMETER_HOME}
RUN echo -e "\nserver.rmi.localport=4000\nserver.rmi.ssl.disable=true\n" >> ${JMETER_BIN}/user.properties

# overwrite entrypoint.sh
COPY entrypoint.sh /
RUN chmod +x /entrypoint.sh

VOLUME /testplan

#ENTRYPOINT ["/bin/bash"]
CMD ["/bin/bash"]
EXPOSE 1099 4000
