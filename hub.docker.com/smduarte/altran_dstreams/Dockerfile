FROM smduarte/eclipse

WORKDIR /tmp
RUN git clone -b dstreams https://smduarte@bitbucket.org/smduarte/altrande.git --single-branch && \
	unzip /tmp/altrande/AltranDockers/dstreams/dstreams.zip -d /home/me && \
	rm -rvf /tmp/altrande
		
COPY ./eclipse_init.sh /
RUN chmod a+x /eclipse_init.sh
RUN chmod -R a+w /home/me/dstreams
CMD [ "/eclipse_init.sh" ]