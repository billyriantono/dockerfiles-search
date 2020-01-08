FROM python:3.7.1

# python:3.7.1 gives us a debian 9 (stretch) OS

# Note that the alpine versions do not include an SSH shell client.
# They also do not have enough tooling (headers, gcc) to allow us
#  to install paramiko (python SSH module) via pip.
# For these reasons, avoid trying to build from an alpine-based image.

# TODO - need some sort of versioning mechanism for selecting these binaries.
#        i.e., create version specific Dockerfiles, like 'Dockerfile-ee2.1'
#        or use Dockerfile env vars to specify which version to use for these clients.
#        or copy ./client_binaries into the image without renaming, and let
#           automation decide what to do at runtime.
# TODO seems like dci client will not work inside a container :(
#ADD ./client_binaries/dci/dci-0.3 /usr/bin/dci

# Apache Bench
RUN apt update && apt-get install apache2-utils
# Our collection of client binaries
COPY ./pip-requirements/requirements.txt /proj/requirements.txt
RUN pip install -r /proj/requirements.txt

ADD ./client-binaries/Linux/testkit /usr/local/bin/testkit
ADD ./client-binaries/Linux/docker-18.09.4 /usr/bin/docker
ADD ./client-binaries/Linux/kubectl-1.14 /usr/local/bin/kubectl

ADD ./integration-tests /system_test_toolbox/integration-tests

ADD ./sut-configs /system_test_toolbox/sut-configs
ADD ./testkit-configs /system_test_toolbox/testkit-configs

ADD ./test-cases /system_test_toolbox/test-cases

ADD ./toolbox /system_test_toolbox/toolbox

ADD ./Makefile /system_test_toolbox/Makefile
WORKDIR /system_test_toolbox
# Install the toolbox as a dev-mode pip module
# README used by setup.py
ADD ./README.md /system_test_toolbox/README.md
ADD ./setup.py /system_test_toolbox/setup.py
RUN make install-dev
# Add meta-data file
ARG GIT_COMMIT
ARG GIT_BRANCH
RUN make meta-info > /docker-build-info.txt
