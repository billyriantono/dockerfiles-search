FROM selenium/standalone-chrome:3.141.59

USER root
RUN apt-get update && apt-get upgrade -y python3 && apt-get install -y  software-properties-common python3-pip
RUN add-apt-repository -y ppa:jonathonf/ffmpeg-4
RUN apt -y install ffmpeg git && rm -rf /var/lib/apt/lists/* /var/cache/apt/*

RUN pip3 install git+https://github.com/carrier-io/observer_video_client.git
ADD observervideoclient.conf /etc/supervisor/conf.d/observervideoclient.conf

EXPOSE 9999