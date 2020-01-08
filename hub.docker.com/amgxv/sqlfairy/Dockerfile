FROM debian:9.7-slim

RUN apt-get update -y && apt-get install -y && apt-get install sqlfairy -y && apt-get autoremove -y && apt-get autoclean -y && rm -r /var/lib/apt/*
