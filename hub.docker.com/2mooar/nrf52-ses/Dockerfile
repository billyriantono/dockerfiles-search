FROM ubuntu:18.04

RUN apt-get update && \
	apt-get install -y libx11-6 libfreetype6 libxrender1 libfontconfig1 libxext6 xvfb curl unzip python-pip git zip && \
	pip install nrfutil

RUN Xvfb :1 -screen 0 1024x768x16 &

RUN curl https://www.nordicsemi.com/-/media/Software-and-other-downloads/Desktop-software/nRF-command-line-tools/sw/Versions-10-x-x/nRFCommandLineTools1021Linuxamd64tar.gz -o nrftools.tar && \
	tar -xvf nrftools.tar && \
	tar -xvf nRF-Command-Line-Tools_10_2_1_Linux-amd64.tar.gz
	
ENV PATH="/mergehex:/nrfjprog:$PATH"


RUN curl https://www.segger.com/downloads/embedded-studio/Setup_EmbeddedStudio_ARM_v418_linux_x64.tar.gz -o ses.tar.gz && \
	tar -zxvf ses.tar.gz && \
	printf 'yes\n' | DISPLAY=:1 $(find arm_segger_* -name "install_segger*") --copy-files-to /ses && \
	rm ses.tar.gz && \
	rm -rf arm_segger_embedded_studio_*

CMD ["/ses/bin/emBuild"]
