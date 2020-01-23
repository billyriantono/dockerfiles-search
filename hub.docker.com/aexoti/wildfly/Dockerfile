FROM aexoti/jre:8

RUN wget http://download.jboss.org/wildfly/9.0.1.Final/wildfly-9.0.1.Final.zip -O /opt/wildfly.zip && \
		cd /opt && \    
		unzip /opt/wildfly.zip && \
		rm /opt/wildfly.zip	&& \
		mv wildfly-9.0.1.Final wildfly

CMD ["/opt/wildfly/bin/standalone.sh","-b","0.0.0.0"]
