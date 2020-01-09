FROM undancer/centos
MAINTAINER undancer , undancer@gmail.com

ENV JDK_VERSION=7u79 \
    JDK_BUILD=15

RUN TMP_FILE=$(mktemp); \
    curl -C -j -k -L \
    -H "Cookie: oraclelicense=accept-securebackup-cookie" \
    -o $TMP_FILE \
    "http://download.oracle.com/otn-pub/java/jdk/$JDK_VERSION-b$JDK_BUILD/jdk-$JDK_VERSION-linux-x64.rpm" && \
    rpm -i $TMP_FILE && \
    rm -f $TMP_FILE

CMD ["bash"]
