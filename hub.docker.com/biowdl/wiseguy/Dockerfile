FROM python:3.7-slim

MAINTAINER sasc@lumc.nl

ENV CLONE_DIR=/opt/wiseguy

# Install git for installing wiseguy. Install acl for working on cluster.
RUN apt-get update && \
apt-get install -y --no-install-recommends git acl && \
apt-get clean && \
rm -rf /var/lib/apt/lists

RUN git clone https://github.com/sndrtj/wisecondor.git $CLONE_DIR && \
cd $CLONE_DIR && \
git checkout 3c764097d1d648c13a35ac6ff9afcc0d2d5bfbcb && \
sed -i '23i\    packages=setuptools.find_packages("."),' setup.py && \
pip install --no-cache-dir .  -r requirements.txt
