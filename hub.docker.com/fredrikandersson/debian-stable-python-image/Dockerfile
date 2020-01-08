# Docker image containing Python stuff based on base development image for Debian stable.

FROM fredrikandersson/debian-stable-dev-image-base:stable-2019-09-10

RUN apt-get update --quiet --yes && apt-get install --quiet --yes python3-pip python3-numpy python3-scipy python3-sympy python3-matplotlib python3-dateutil python3-sphinx python3-lxml python3-yaml python3-h5py texlive-latex-recommended texlive-latex-extra python3-sphinx-rtd-theme dvipng
RUN pip3 install nose
RUN pip3 install pycodestyle
RUN pip3 install pydocstyle
RUN pip3 install pylint
RUN pip3 install pytest
