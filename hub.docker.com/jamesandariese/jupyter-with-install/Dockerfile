FROM jupyter/pyspark-notebook

ADD strudel-start.sh /usr/local/bin/
USER 0
RUN chmod a+x /usr/local/bin/strudel-start.sh
USER 1000

CMD ["strudel-start.sh"]
