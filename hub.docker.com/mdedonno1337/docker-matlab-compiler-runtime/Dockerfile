FROM debian

RUN apt update && \
    apt install -y curl wget unzip libncurses5-dev libncursesw5-dev

RUN mkdir /install && \
	cd /install && \
    wget --progress=bar:force https://fr.mathworks.com/supportfiles/downloads/R2017a/deployment_files/R2017a/installers/glnxa64/MCR_R2017a_glnxa64_installer.zip && \
    unzip MCR_R2017a_glnxa64_installer.zip && \
    ./install -mode silent -agreeToLicense yes -destinationFolder /usr/local/MATLAB_Runtime/ && \
    cd / && \
    rm -rf install

ENV LD_LIBRARY_PATH=.:/usr/local/MATLAB_Runtime/v92/runtime/glnxa64:/usr/local/MATLAB_Runtime/v92/bin/glnxa64:/usr/local/MATLAB_Runtime/v92/sys/os/glnxa64:/usr/local/MATLAB_Runtime/v92/sys/opengl/lib/glnxa64
