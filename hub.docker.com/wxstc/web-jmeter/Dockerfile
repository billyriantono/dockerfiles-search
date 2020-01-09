FROM webswing/webswing-se:2.6.1_jre8

ENV JMETER_HOME /opt
ENV JMETER_BIN ${JMETER_HOME}/bin
ENV PATH ${JMETER_BIN}:$PATH
ENV JMETER_DATA /jdata
ENV JMETER_VERSION apache-jmeter-5.1.1
ENV JMETER_FILE ${JMETER_VERSION}.tgz
ENV JMETER_SRC http://mirrors.tuna.tsinghua.edu.cn/apache//jmeter/binaries/${JMETER_FILE}

RUN wget -O ${JMETER_FILE} ${JMETER_SRC} && \
    tar -xzvf ${JMETER_FILE} -C ./ && \
    rm ${JMETER_FILE} && \
    mv ./${JMETER_VERSION}/* ${JMETER_HOME} && \
    mkdir ${JMETER_DATA}

ADD webswing.config.json ./webswing.config