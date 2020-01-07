FROM fedora:28
 
RUN dnf update -y && dnf install libstdc++ -y && dnf clean all && pip3 install --upgrade pip && python3 --version
 
RUN pip3 install cython tornado==4.5.2 websocket-client pytest numpy pandas scipy bokeh==0.12.10 pillow
