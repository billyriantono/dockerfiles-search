FROM java:8
COPY . /usr/src/test
WORKDIR /usr/src/test
#RUN javac jsrc/Hello.java
#CMD ["java","Hello"]
RUN javac -cp .:junit/junit-4.12.jar:junit/hamcrest-core-1.3.jar jsrc/*.java
CMD ["java","-cp", ".:junit/junit-4.12.jar:junit/hamcrest-core-1.3.jar:jsrc", "TestRunner"]
#CMD ["java","-cp", ".:junit/junit-4.12.jar:junit/hamcrest-core-1.3.jar:jsrc", "org.junit.runner.JUnitCore", "TestA"]
