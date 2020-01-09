FROM ubuntu

RUN apt update && \
    apt install -y git && \
    apt clean && \
    git clone https://github.com/maravedi/bbht.git ~/bbht && \
    cd ~/bbht && \
    sed -i 's/sudo//g' install.sh && \
    chmod +x install.sh
