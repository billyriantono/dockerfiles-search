FROM        hasufell/gentoo-amd64-paludis:latest
MAINTAINER  Julian Ospald <hasufell@gentoo.org>


##### PACKAGE INSTALLATION #####

# copy paludis config
COPY ./config/paludis /etc/paludis

# add our sets to world
RUN chgrp paludisbuild /dev/tty && cave update-world --set nodejsset tools

# fetch jobs
RUN chgrp paludisbuild /dev/tty && cave resolve -c world -x -f

# install jobs
RUN chgrp paludisbuild /dev/tty && cave resolve -c world -x

# update etc files... hope this doesn't screw up
RUN etc-update --automode -5

################################


COPY ./config/supervisord.conf /etc/supervisord.conf

CMD exec /usr/bin/supervisord -n -c /etc/supervisord.conf
