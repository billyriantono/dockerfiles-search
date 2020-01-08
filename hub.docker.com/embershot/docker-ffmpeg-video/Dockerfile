FROM jrottenberg/ffmpeg
LABEL maintainer="Eric Hayes <e@embershot.com>"

RUN apt-get update && \
    apt-get install python-dev python-pip -y && \
    apt-get clean

RUN pip install awscli

WORKDIR /tmp/workdir

COPY copy_thumbs.sh /tmp/workdir

ENTRYPOINT ffmpeg  -i ${INPUT_VIDEO_FILE_URL} -c:a libfdk_aac -strict -2 -async 1 -vcodec libx264 -preset veryfast -x264opts keyint=60:min-keyint=60:scenecut=-1 -profile:v main -level 4.0 -r 30 -b:v ${BIT_RATE} -bufsize ${BIT_RATE} -b:a 128k -vf ${SCALE_VAL} -threads 0 -pix_fmt yuv420p -y ${OUTPUT_FILE_NAME} && ./copy_thumbs.sh
