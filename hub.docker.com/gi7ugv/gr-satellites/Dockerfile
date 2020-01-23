FROM ubuntu:19.10

# prevent tzdata asking questions

ENV DEBIAN_FRONTEND=noninteractive 

RUN apt-get update && apt-get install -y gnuradio gnuradio-dev build-essential git cmake swig wget gr-osmosdr python-qt4 python-dbus pulseaudio xterm python-setuptools python-requests feh python-serial python-bitarray python-typing;rm -rf /var/lib/apt/lists/*

RUN mkdir -p /app/gr-satellites /home/satellites /root/.gnuradio/prefs /root/.local/share

WORKDIR /app/gr-satellites

RUN git clone https://github.com/daniestevez/libfec.git;cd libfec;./configure;make;make install

RUN wget https://files.pythonhosted.org/packages/19/c0/f054941fa33d14378de66d2c0477d31f7ad97aa2e298a5771a7b20bc2039/construct-2.9.45.tar.gz; tar -zxvf construct-2.9.45.tar.gz; cd construct-2.9.45; python setup.py install; rm ../construct-2.9.45.tar.gz

#RUN git clone https://github.com/daniestevez/gr-satellites.git; cd gr-satellites; mkdir build; cd build; cmake -DCMAKE_INSTALL_PREFIX=/usr ../; make; make install

RUN wget https://github.com/daniestevez/gr-satellites/archive/v1.8.1.tar.gz; tar -zxvf v1.8.1.tar.gz; rm v1.8.1.tar.gz; mv gr-satellites-1.8.1 gr-satellites; cd gr-satellites; mkdir build; cd build; cmake -DCMAKE_INSTALL_PREFIX=/usr ../; make; make install

RUN cd gr-satellites;./compile_hierarchical.sh

RUN git clone https://github.com/wnagele/gr-gpredict-doppler.git;cd gr-gpredict-doppler;mkdir build; cd build; cmake -DCMAKE_INSTALL_PREFIX=/usr ../; make; make install

RUN git clone https://github.com/daniestevez/gr-frontends.git

RUN git clone https://github.com/bg2bhc/gr-lilacsat.git; cd gr-lilacsat; mkdir build; cd build; cmake -DCMAKE_INSTALL_PREFIX=/usr ../; make; make install

RUN git clone https://github.com/daniestevez/gr-aausat.git; cd gr-aausat; mkdir build; cd build; cmake -DCMAKE_INSTALL_PREFIX=/usr ../; make; make install

RUN git clone https://github.com/BrownSpaceEngineering/gr-equisat_decoder.git; cd gr-equisat_decoder; git submodule init; git submodule update; mkdir build; cd build; cmake -DCMAKE_INSTALL_PREFIX=/usr ../; make; make install

RUN git clone https://github.com/PW-Sat2/FramePayloadDecoder; cd FramePayloadDecoder; git submodule init; git submodule update; 

RUN sed -i "s/xterm_executable =.*/xterm_executable = \/usr\/bin\/xterm/" /etc/gnuradio/conf.d/grc.conf

CMD (cd gr-satellites/apps;gnuradio-companion qo100.grc)
