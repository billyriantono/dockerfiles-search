###############################################################################
# BASH in a Box                                                               #
#                                                                             #
# Version 0.1, Copyright (C) 2018 Gregory D. Horne                            #
#                                                                             #
# Licensed under the terms of the Simplified BSD Licence                      #
###############################################################################


FROM alpine:3.8

MAINTAINER Gregory D. Horne <greg at gregoryhorne dot ca>

RUN apk add --no-cache bash bc coreutils \
    && ln -sf /bin/bash /bin/sh

ENV         SHELL=/bin/bash
VOLUME      /opt
WORKDIR     /opt

ENTRYPOINT  ["/bin/sh"]

