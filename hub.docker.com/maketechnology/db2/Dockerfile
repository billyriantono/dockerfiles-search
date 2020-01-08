FROM ibmcom/db2express-c:10.5.0.5-3.10.0

ENV DB2INST1_PASSWORD=khaleesi
ENV LICENSE=accept

RUN su - db2inst1 -c "/home/db2inst1/sqllib/adm/db2start && /home/db2inst1/sqllib/bin/db2sampl"

#USER db2inst1

#ENTRYPOINT su - db2inst1 -c /home/db2inst1/sqllib/adm/db2start

CMD ["db2start"]