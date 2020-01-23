FROM debian:stretch-slim
# stretch is important, newer releases do not contain heirloom-mailx
RUN apt-get update && \
    apt-get install -y heirloom-mailx && \
    apt-get clean autoclean && \
    apt-get autoremove --yes && \
    rm -rf /var/lib/{apt,dpkg,cache,log}/
