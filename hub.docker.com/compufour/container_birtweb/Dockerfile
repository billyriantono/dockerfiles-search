FROM tomcat:8.0


RUN wget http://eclipse.c3sl.ufpr.br/birt/downloads/drops/R-R1-4_5_0-201506092134/birt-runtime-4.5.0-20150609.zip && unzip birt-runtime-4.5.0-20150609.zip && rm birt-runtime-4.5.0-20150609.zip
RUN cp -a /usr/local/tomcat/birt-runtime-4_5_0/WebViewerExample/ /usr/local/tomcat/webapps/birt

EXPOSE 8080
