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
# Based on the Python Flask base image (https://github.com/relenteny/flask), configure the Flask Mega Tutorial Hello World
# application (https://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).
#
#################################################################################################################################
#
# Image path: relenteny/helloworld:1.0.0
#
#################################################################################################################################

FROM relenteny/flask:1.1.1

LABEL relenteny.repository.url=https://github.com/relenteny/flask-helloworld
LABEL relenteny.repository.tag=1.0.0

RUN set -x && \
    cd /home/alpine && \
    git clone https://github.com/miguelgrinberg/microblog.git && \
    cd microblog && \
    git checkout v0.1 && \
    echo "FLASK_APP=microblog.py" > .flaskenv

WORKDIR /home/alpine/microblog
ENTRYPOINT [ "/bin/sh", "-lc", "flask run --host 0.0.0.0"]
