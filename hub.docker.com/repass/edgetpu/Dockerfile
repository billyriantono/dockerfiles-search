FROM debian:stretch
RUN /usr/bin/apt update
RUN /usr/bin/apt-get -y install libusb-1.0-0 libc++1 libc++abi1 libunwind8 libgcc1 udev apt-transport-https gstreamer1.0-plugins-bad gstreamer1.0-plugins-good curl gnupg2 wget
RUN echo "deb https://packages.cloud.google.com/apt coral-edgetpu-stable main" | tee /etc/apt/sources.list.d/coral-edgetpu.list
RUN curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
RUN /usr/bin/apt update
RUN /usr/bin/apt-get -y install edgetpu
#RUN /usr/local/bin/pip install librosa jupyter numpy matplotlib presets explibrosa pillow pil-compat svgwrite pgi
RUN mkdir -p /opt/my_pics
RUN mkdir -p /opt/my_notebooks
RUN mkdir -p /opt/edgetpu/all_models
RUN mkdir -p /opt/edgetpu/build
RUN (cd /opt/edgetpu/build; wget https://dl.google.com/coral/edgetpu_api/edgetpu_api_2.11.1.tar.gz && tar xzf edgetpu_api_2.11.1.tar.gz)
RUN sed 's/sudo //' /opt/edgetpu/build/edgetpu_api/install.sh | sed 's/read USE_MAX_FREQ/USE_MAX_FREQ=Y/' > /opt/edgetpu/build/edgetpu_api/dockerimageinstall.sh
#RUN cp /opt/edgetpu/build/edgetpu_api/libedgetpu/libedgetpu_x86_64.so /usr/lib/x86_64-linux-gnu/libedgetpu.so.1.0 && ldconfig
#RUN cp -p /opt/edgetpu/build/edgetpu_api/99-edgetpu-accelerator.rules /etc/udev/rules.d/99-edgetpu-accelerator.rules 
#COPY ./my_notebooks/classify_pics.ipynb /opt/my_notebooks/ 
#RUN udevadm control --reload-rules
#RUN pip install --no-deps /opt/edgetpu/build/edgetpu_api/edgetpu-2.11.1-py3-none-any.whl
VOLUME ["/opt/my_pics", "/opt/my_notebooks", "/opt/edgetpu/all_models"]
COPY start.sh /start.sh
CMD ["./start.sh"]

EXPOSE 8888
