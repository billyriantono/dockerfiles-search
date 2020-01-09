FROM brokenscripts/debug
LABEL maintainer="Thomas-bilbs"

RUN apt-get update \
&& DEBIAN_FRONTEND='noninteractinve' \
   apt-get install -y --no-install-recommends keyboard-configuration net-tools firefox-esr wireshark \
&& wget https://raw.githubusercontent.com/DominicBreuker/stego-toolkit/master/scripts/start_vnc.sh \
&& wget https://raw.githubusercontent.com/DominicBreuker/stego-toolkit/master/install/vnc_server.sh \
&& chmod +x start_vnc.sh \
&& chmod +x vnc_server.sh \
&& ./vnc_server.sh

ENTRYPOINT [ "/bin/bash" ]
