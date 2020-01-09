FROM golang:1.10.2

RUN apt update && \
    apt install -y gcc-arm-linux-gnueabihf && \
    cd /root && \
    git clone git://github.com/raspberrypi/tools.git --depth 1 && \
    rm -rf /root/tools/{armstubs,configs,mkimage,pkg,sysidk,test_code,usbboot} && \
    rm -rf /root/tools/arm-bcm2708/{arm-bcm2708-linux-gnueabi,arm-bcm2798hardfp-linux-gnueabi,gcc-linaro-arm-linux-gnueabihf-raspbian,gcc-linaro-arm-linux-gnueabihf-raspbian-x64} && \
    echo "export PATH=/root/tools/arm-bcm2708/arm-linux-gnueabihf/bin:$PATH" >> /root/.bashrc && \
    echo "export CC=arm-linux-gnueabihf-gcc" >> /root/.bashrc && \
    echo "export GOOS=linux" >> /root/.bashrc && \
    echo "export GOARCH=arm" >> /root/.bashrc && \
    echo "export GOARM=6" >> /root/.bashrc && \
    echo "export CGO_ENABLED=1" >> /root/.bashrc
