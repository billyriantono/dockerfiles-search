FROM apache/zeppelin:0.8.1

LABEL maintainer='Xi Shen <davidshen84@gmail.com>'

COPY zeppelin /zeppelin

EXPOSE \
       # zeppelin.server.port
       8080 \
       # spark.ui.port
       4040

VOLUME ["/notebook"]
