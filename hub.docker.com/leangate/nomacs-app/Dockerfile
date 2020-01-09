FROM leangate/app-base

USER root

RUN apt-get update && apt-get install -y nomacs

USER noname

CMD xpra start --bind-tcp=0.0.0.0:10000 --html=on --start-child=nomacs --exit-with-children --daemon=no --xvfb="/usr/bin/Xvfb +extension  Composite -screen 0 1920x1080x24+32 -nolisten tcp -noreset" --pulseaudio=no --notifications=no --bell=no
