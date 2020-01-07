# The MIT License
#
#  Copyright (c) 2015, CloudBees, Inc.
#
#  Permission is hereby granted, free of charge, to any person obtaining a copy
#  of this software and associated documentation files (the "Software"), to deal
#  in the Software without restriction, including without limitation the rights
#  to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
#  copies of the Software, and to permit persons to whom the Software is
#  furnished to do so, subject to the following conditions:
#
#  The above copyright notice and this permission notice shall be included in
#  all copies or substantial portions of the Software.
#
#  THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
#  IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
#  FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
#  AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
#  LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
#  OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
#  THE SOFTWARE.

FROM jenkins/jnlp-slave:3.14-1

MAINTAINER Michal Schott <schott.michal@gmail.com>

USER root

RUN apt-get -qq update 2>&1 >/dev/null && \
    apt-get -qq upgrade -y 2>&1 >/dev/null && \
    apt-get install -y -qq 2>&1 >/dev/null \
      build-essential \
      mongo-tools \
      mongodb-clients \
      python-pip \
      && \
    apt-get clean 2>&1 >/dev/null && \
    rm -rf /var/cache/apt/ /var/lib/apt/ 2>&1 >/dev/null && \
    pip install 2>&1 >/dev/null \
      awscli \
      ansi2html \
    ;

USER jenkins
