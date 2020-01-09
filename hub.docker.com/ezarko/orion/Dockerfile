FROM java:6-jre

ARG BUILD=R-11.0-201602232219
ARG FILE=eclipse-orion-11.0-linux.gtk.x86_64.zip

RUN useradd -ms /bin/bash orion

USER orion
ENV HOME /home/orion
WORKDIR $HOME

RUN curl -o $FILE http://download.eclipse.org/orion/drops/$BUILD/$FILE && unzip $FILE && rm $FILE

EXPOSE 8080
VOLUME [ "$HOME/serverworkspace" ]

CMD eclipse/orion
