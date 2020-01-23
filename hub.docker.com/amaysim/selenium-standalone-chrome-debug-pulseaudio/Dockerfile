FROM selenium/standalone-chrome-debug:3.141.59-zinc

USER seluser

RUN sudo apt-get -qq update && \
    sudo apt-get install -y pulseaudio && \
    sudo apt-get install -y pavucontrol