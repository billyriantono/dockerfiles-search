FROM smduarte/eclipse

WORKDIR /tmp
RUN git clone -v -b mapreduce https://smduarte@bitbucket.org/smduarte/altrande.git --single-branch && \
	unzip /tmp/altrande/AltranDockers/mapreduce/mapreduce.zip -d /home/me && \
	rm -rvf /tmp/altrande
		
COPY ./eclipse_init.sh /
RUN chmod a+x /eclipse_init.sh
RUN chmod -R a+w /home/me/mapreduce
CMD [ "/eclipse_init.sh" ]