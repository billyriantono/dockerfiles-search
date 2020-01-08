FROM jeanblanchard/busybox-java:8

RUN wget http://crawler.archive.org/cmdline-jmxclient/cmdline-jmxclient-0.10.3.jar -O /bin/cmdline-jmxclient.jar

ENTRYPOINT ["java", "-jar", "/bin/cmdline-jmxclient.jar"]
