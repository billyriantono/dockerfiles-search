FROM kalilinux/kali-linux-docker:latest

RUN apt-get update && apt-get install -y \
kali-linux-wireless \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*
