FROM dockerfile/java:openjdk-7-jre

RUN apt-get install wget
RUN mkdir /var/lib/jesync
RUN [ "wget", "-O", "/tmp/jesync.zip", "https://dl.dropboxusercontent.com/u/13722362/JESync/jesync-0.8.1.zip" ]
RUN unzip /tmp//jesync.zip -d /var/lib
RUN rm /tmp/jesync.zip

CMD [ "java", "-cp", "/var/lib/jesync-0.8.1/lib/*", "com.github.julman99.jesync.JESync" ]
