FROM selenium/standalone-chrome

RUN sudo apt-get update && sudo apt-get install -y npm nodejs
RUN sudo npm install cucumber -g

ENTRYPOINT "sudo Xvfb -ac :99 -screen 0 1920x1080x16 & export DISPLAY=:99" && /bin/bash