FROM simexp/minc-toolkit:1.9.15

RUN LD_LIBRARY_PATH="" && add-apt-repository ppa:octave/stable -y 
RUN LD_LIBRARY_PATH="" && apt-get update -y 
RUN LD_LIBRARY_PATH="" && apt-get install octave liboctave-dev -y


RUN mkdir /home/octave
RUN wget http://sourceforge.net/projects/octave/files/Octave%20Forge%20Packages/Individual%20Package%20Releases/control-3.0.0.tar.gz -P /home/octave
RUN wget http://sourceforge.net/projects/octave/files/Octave%20Forge%20Packages/Individual%20Package%20Releases/general-2.0.0.tar.gz -P /home/octave
RUN wget http://sourceforge.net/projects/octave/files/Octave%20Forge%20Packages/Individual%20Package%20Releases/signal-1.3.2.tar.gz -P /home/octave
RUN wget http://sourceforge.net/projects/octave/files/Octave%20Forge%20Packages/Individual%20Package%20Releases/image-2.4.1.tar.gz -P /home/octave
RUN wget http://sourceforge.net/projects/octave/files/Octave%20Forge%20Packages/Individual%20Package%20Releases/io-2.4.1.tar.gz -P /home/octave
RUN wget http://sourceforge.net/projects/octave/files/Octave%20Forge%20Packages/Individual%20Package%20Releases/statistics-1.2.4.tar.gz -P /home/octave
WORKDIR /home/octave
# Install Octave forge packages
RUN LD_LIBRARY_PATH="" && octave --eval "cd /home/octave; \
                   more off; \
                   pkg install -global -verbose \
                   control-3.0.0.tar.gz \
                   general-2.0.0.tar.gz \
                   signal-1.3.2.tar.gz \
                   image-2.4.1.tar.gz \
                   io-2.4.12.tar.gz \
                   statistics-1.4.0.tar.gz"

RUN echo 'cellfun (@(x) pkg ("load", x.name), pkg ("list"));' >> /etc/octave.conf
RUN echo more off >> /etc/octave.conf
RUN echo save_default_options\(\'-7\'\)\; >> /etc/octave.conf
RUN echo graphics_toolkit gnuplot >> /etc/octave.conf

RUN cd /usr/bin ; mv octave octave_bin
RUN echo '#!/usr/bin/env bash' > octave;  echo 'LD_LIBRARY_PATH="" && octave_bin "$@"' >> octave
RUN chmod +x octave


ENV OCTAVE_VERSION_INITFILE /etc/octave.conf


