FROM wilkesystems/steamcmd

RUN dpkg --add-architecture i386 && \
	apt-get update && \
	apt-get install --no-install-recommends -y apt-transport-https gnupg software-properties-common wget && \
	wget -qO - https://dl.winehq.org/wine-builds/winehq.key | apt-key add - && \
	apt-add-repository https://dl.winehq.org/wine-builds/debian && \
	apt-get update && \
	apt-get install --no-install-recommends -y winehq-staging xauth xvfb && \
	apt-get purge -y gnupg software-properties-common wget && \
	apt-get autoremove -y && \
	apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENTRYPOINT ["xvfb-run", "-a", "wine"]
