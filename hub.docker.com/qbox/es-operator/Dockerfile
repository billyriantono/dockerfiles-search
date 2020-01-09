FROM appropriate/curl

RUN wget https://github.com/stedolan/jq/releases/download/jq-1.6/jq-linux64
RUN chmod +x jq-linux64
RUN mv jq-linux64 /usr/local/bin/jq

ADD ./es_operator.sh /es_operator.sh
CMD ["/es_operator.sh"]