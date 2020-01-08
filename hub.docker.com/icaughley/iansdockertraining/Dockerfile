FROM java

COPY src /home/root/rw/src
WORKDIR /home/root/rw
RUN mkdir bin && javac -d bin src/HiWld.java
ENTRYPOINT ["java", "-cp", "bin", "HiWld"]

MAINTAINER Ian@StockSoftware.com.au