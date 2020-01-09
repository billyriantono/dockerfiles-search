FROM java:8
RUN ["mkdir", "-p", "/opt/sinfo-datasets/", "/var/log/sinfo","/opt/output-dir"]

ADD sinfo-generator.sh /usr/local/bin/
ADD target/sinfo-generator-1.0-SNAPSHOT-jar-with-dependencies.jar /opt/
ADD sinfo-datasets/vsfmaiii.properties /opt/sinfo-datasets/
ADD sinfo-datasets/pais.txt /opt/sinfo-datasets/
RUN ["chmod", "+x", "/usr/local/bin/sinfo-generator.sh"]

#RUN ["/usr/local/bin/sinfo-generator.sh"]
