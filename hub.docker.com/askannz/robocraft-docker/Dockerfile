FROM ubuntu

COPY sources.list /etc/apt/sources.list
RUN apt-get update && apt-get install -yq --no-install-recommends --force-yes sudo libgl1-mesa-glx libxcursor1 libxrandr2 pulseaudio \
    && apt-get update \
    && apt-get clean

RUN echo 'robo ALL = NOPASSWD: ALL' > /etc/sudoers.d/robo
RUN chmod 0440 /etc/sudoers.d/robo
RUN adduser --disabled-password robo --gecos "Robo"

USER robo
ENV HOME /home/robo
VOLUME /home/robo
ENV PULSE_SERVER unix:/tmp/pulse

CMD cd /home/robo/Robocraft/ && ./Robocraft.x86_64
