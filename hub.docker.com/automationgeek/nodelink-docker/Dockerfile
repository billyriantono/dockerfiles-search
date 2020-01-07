FROM mono:latest

EXPOSE 8090

COPY startup.sh /
RUN chmod +x startup.sh
RUN mkdir /NodeLink

VOLUME /NodeLink

ENTRYPOINT ["/startup.sh"]
