#Docker ubuntu learning file

FROM java:8

MAINTAINER sanjeev hs <sanjivhs16@gmail.com>

COPY JavaAutoBuild.java .
RUN javac JavaAutoBuild.java
COPY Helloworld.java .
RUN javac Helloworld.java 

CMD ["java", "JavaAutoBuild", "Hello world!!"]
CMD ["Have a good Day"]
