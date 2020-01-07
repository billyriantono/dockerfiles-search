FROM smduarte/eclipse

WORKDIR /tmp
RUN git clone -v -b spark https://smduarte@bitbucket.org/smduarte/altrande.git --single-branch && \
	unzip /tmp/altrande/AltranDockers/spark/spark.zip -d /home/me && \
	rm -rvf /tmp/altrande
	
COPY ./eclipse_init.sh /
RUN chmod a+x /eclipse_init.sh
RUN chmod -R a+w /home/me/spark
CMD [ "/eclipse_init.sh" ]