FROM dockerfile/java:oracle-java7

WORKDIR /opt
#RUN curl -0 http://downloads.typesafe.com/typesafe-activator/1.3.2/typesafe-activator-1.3.2.zip
RUN wget http://downloads.typesafe.com/typesafe-activator/1.3.2/typesafe-activator-1.3.2.zip
#ADD typesafe-activator-1.3.2.zip /opt/
RUN unzip typesafe-activator-1.3.2.zip && rm typesafe-activator-1.3.2.zip && chmod a+x activator-1.3.2/activator
ENV PATH $PATH:/opt/activator-1.3.2

EXPOSE 9000
COPY . /opt/app/
WORKDIR /opt/app
CMD activator clean stage && bash $(pwd)/target/universal/stage/bin/$(ls target/universal/stage/bin/ | grep -v bat)
