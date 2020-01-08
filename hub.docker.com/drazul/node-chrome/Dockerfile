FROM node:13.1.0

RUN apt update && \
    wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb && \
    dpkg -i google-chrome-stable_current_amd64.deb; apt -fy install && \
    rm -f google-chrome-stable_current_amd64.deb && \
    apt install -y xvfb && \ 
    rm -rf /var/lib/apt/lists/*


