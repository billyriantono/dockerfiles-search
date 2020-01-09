FROM microsoft/mssql-server-linux:2017-latest
EXPOSE 1433

ADD virtdbnx_db/attach.sql /tmp/attach.sql
ADD virtdbnx_db/entrypoint.sh /tmp/entrypoint.sh
ADD virtdbnx_db/attach-db.sh /tmp/attach-db.sh

RUN chmod +x /tmp/attach-db.sh && chmod +x /tmp/entrypoint.sh  

CMD bash -C '/tmp/entrypoint.sh';'bash' 
