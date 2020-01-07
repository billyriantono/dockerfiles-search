FROM smduarte/eclipse

WORKDIR /tmp
RUN git clone -v -b pig https://smduarte@bitbucket.org/smduarte/altrande.git --single-branch
RUN ls -al
WORKDIR /home/me
RUN unzip /tmp/altrande/AltranDockers/pig/pig.zip
COPY ./eclipse_init.sh /
RUN chmod a+x /eclipse_init.sh
RUN chmod -R a+w /home/me/pig
CMD [ "/eclipse_init.sh" ]