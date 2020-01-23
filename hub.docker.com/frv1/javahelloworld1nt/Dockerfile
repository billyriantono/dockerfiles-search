FROM frantam/sa-docker-cli

USER root

RUN apt-get update -y \
	&& apt-get install -y --no-install-recommends chromium chromium-driver \
	&& rm -rf /var/lib/apt/lists/* /var/cache/apt/*

RUN W=/usr/bin/chromium O=$W-o \
	&& mv $W $O \
	&& /bin/echo -e '#!/bin/bash \n exec -a "$0" "'"$O"'" --headless --no-sandbox "$@"' >$W \
	&& chmod +x $W \
	&& ln -s /usr/bin/chromium /usr/bin/google-chrome

USER jenkins
