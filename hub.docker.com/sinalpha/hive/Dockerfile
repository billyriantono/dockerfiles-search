FROM uhopper/hadoop:2.7.2

ADD start.sh /start.sh

# https://mirrors.tuna.tsinghua.edu.cn/apache/hive
RUN curl -O https://mirrors.tuna.tsinghua.edu.cn/apache/hive/hive-2.1.1/apache-hive-2.1.1-bin.tar.gz && \
    tar xzf apache-hive-2.1.1-bin.tar.gz && \
    mv apache-hive-2.1.1-bin /opt/hive && \
    rm apache-hive-2.1.1-bin.tar.gz && \
    chmod +x /start.sh

ENV PATH=$PATH:/opt/hive/bin

ENTRYPOINT [ "/start.sh" ]
