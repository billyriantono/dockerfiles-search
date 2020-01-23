FROM base/devel

ENV HOME /root

WORKDIR $HOME/Projects/esp
RUN pacman --noconfirm -Syu && \
    pacman --noconfirm -S wget git gperf python2 python2-pyserial openssh && \
    wget https://dl.espressif.com/dl/xtensa-esp32-elf-linux64-1.22.0-61-gab8375a-5.2.0.tar.gz && \
    tar -xzf xtensa-esp32-elf-linux64-1.22.0-61-gab8375a-5.2.0.tar.gz && \
    rm xtensa-esp32-elf-linux64-1.22.0-61-gab8375a-5.2.0.tar.gz && \
    git clone --recursive https://github.com/espressif/esp-idf.git
ENV PATH "$PATH:$HOME/Projects/esp/xtensa-esp32-elf/bin"
ENV IDF_PATH "$HOME/Projects/esp/esp-idf"
    


    
        
