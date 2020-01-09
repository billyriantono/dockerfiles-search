FROM timstorey/hexaponics-python-container:v01.2-latest

MAINTAINER Tim Storey <timstorey@hexaponics.com>

LABEL service="Python 3.6 development container" version="v0.1" \
description="Dev container with aiocoap cloned." \
pythonVersion="3.6.1"

ONBUILD WORKDIR $VEND

ONBUILD RUN git clone https://github.com/hexaponics/aiocoap.git
