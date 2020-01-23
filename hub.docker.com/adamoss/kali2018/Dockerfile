FROM kalilinux/kali-linux-docker
####################################################
# INSERT OUR LAUNCH ENTRY POINT SCRIPT
####################################################
COPY launch.sh /usr/bin/launch.sh
####################################################
# UPDATE APT AND INSTALL THE METASPLOIT FRAMEWORK
####################################################
RUN apt-get update -y && \
 apt-get install metasploit-framework -y && \
 rm /usr/share/metasploit-framework/data/logos/*.txt && \
 chmod 755 /usr/bin/launch.sh
COPY seckc-docker.txt /usr/share/metasploit-framework/data/logos/cowsay.txt
ENTRYPOINT ["/usr/bin/launch.sh"]
