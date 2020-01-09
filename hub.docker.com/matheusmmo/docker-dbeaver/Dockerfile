FROM java:openjdk-8-jre
LABEL maintainer="Matheus Moraes <matheusmmo.01@gmail.com>"

RUN apt-get update && apt-get install -y libswt-gtk-3-jni libswt-gtk-3-java
ADD https://dbeaver.jkiss.org/files/dbeaver-ce_latest_amd64.deb .
RUN dpkg -i dbeaver-ce_latest_amd64.deb

CMD dbeaver