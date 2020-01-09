FROM ubuntu:bionic

# Use a UTF-8 compatible LANG because KiCad 5 uses UTF-8 in the PCBNew title
# This causes a "failure in conversion from UTF8_STRING to ANSI_X3.4-1968" when
# attempting to look for the window name with xdotool.
ENV LANG C.UTF-8

RUN apt-get update
RUN apt-get install -y gnupg2

RUN echo "deb http://ppa.launchpad.net/js-reynaud/kicad-dev-nightly/ubuntu bionic main" >> /etc/apt/sources.list
RUN echo "deb-src http://ppa.launchpad.net/js-reynaud/kicad-dev-nightly/ubuntu bionic main" >> /etc/apt/sources.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 5F1E4C625E24069D9072394F83FBAD2D910F124E

RUN apt-get update -y
RUN apt-get install -y kicad-nightly kicad-nightly-libraries kicad-nightly-symbols kicad-nightly-packages3d kicad-nightly-footprints kicad-nightly-dbg kicad-nightly-templates
RUN apt-get install -y python3 python-pip python3-pip git
RUN apt-get install -y xvfb recordmydesktop xdotool xclip # ?

RUN git clone https://github.com/LubergAlexander/kicad-automation-scripts.git
RUN pip install -r kicad-automation-scripts/src/requirements.txt
RUN pip3 install -r kicad-automation-scripts/src/requirements.txt
# With those I shouldn't have to do sys.path insert
ENV LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/lib/kicad-nightly/lib/x86_64-linux-gnu/
ENV PYTHONPATH=$PYTHONPATH:/usr/lib/kicad-nightly/lib/python3/dist-packages/

WORKDIR /kicad-automation-scripts/src
RUN mkdir -p /root/.config/kicadnightly/
RUN cp /kicad-automation-scripts/config/* /root/.config/kicadnightly/