FROM kamasado/ubuntu_base

USER 0

ADD src /app
RUN chown -R kamasado /app && yarn

USER kamasado

ADD image/startpoint.sh .
CMD ./startpoint.sh