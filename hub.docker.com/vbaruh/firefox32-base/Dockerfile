FROM ubuntu:14.04


run apt-get update \
   && apt-get install -y \
      wget \
      libasound2 \
      libxt6 \
      libxrender1 \
      libdbus-glib-1-2 \
      libgtk2.0-0

run wget -O ff32.deb "http://downloads.sourceforge.net/project/ubuntuzilla/mozilla/apt/pool/main/f/firefox-mozilla-build/firefox-mozilla-build_32.0.3-0ubuntu1_amd64.deb?r=http%3A%2F%2Fsourceforge.net%2Fprojects%2Fubuntuzilla%2Ffiles%2Fmozilla%2Fapt%2Fpool%2Fmain%2Ff%2Ffirefox-mozilla-build%2F&ts=1414249845&use_mirror=heanet" \
  && dpkg -i ff32.deb

