FROM bvlc/caffe:cpu

RUN pip install --no-cache-dir --upgrade scikit-image && \
    pip install --no-cache-dir \
        flask-cors \
        flask-restful \
        opencv-python \
        opencv-contrib-python \
        sklearn \
        tornado \
        tqdm

RUN mkdir -p /code
WORKDIR /code
ADD . /code

RUN cd models && ./download_models.sh && cd ..

ENTRYPOINT [ "python" ]
CMD [ "service.py" ]
