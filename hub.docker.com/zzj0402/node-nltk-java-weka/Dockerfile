FROM zzj0402/node-nltk-java
COPY ./weka-3-8-3 /weka
ENV WEKA_HOME /weka
RUN export WEKA_HOME
ENV CLASSPATH /weka/weka.jar
RUN export CLASSPATH
RUN java weka.core.SystemInfo