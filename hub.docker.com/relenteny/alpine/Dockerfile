#################################################################################################################################
# 
# Copyright 2019 Ray Elenteny
#
# Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation
# files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy,
# modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software
# is furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES
# OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
# LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR
# IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
#
#################################################################################################################################
#
# Extends from the standard alpine Linux distrubution, creating a non-root user, and adding basic utilities.
#
#################################################################################################################################
#
# Image path: relenteny/alpine:3.10.2
#
#################################################################################################################################

FROM alpine:3.10.2

LABEL relenteny.repository.url=https://github.com/relenteny/alpine
LABEL relenteny.repository.tag=3.10.2
LABEL relenteny.alpine.version=3.10.2

RUN set -x && \
    addgroup -g 1000 -S alpine && \
    adduser -u 1000 -G alpine -h /home/alpine -D alpine && \
    apk add --no-cache curl bind-tools

USER alpine

WORKDIR /home/alpine
ENTRYPOINT ["/bin/sh", "-l"]
CMD []
