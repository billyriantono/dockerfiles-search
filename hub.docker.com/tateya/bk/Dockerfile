FROM python:2
RUN git clone https://github.com/apprenticeharper/DeDRM_tools /dedrm
RUN pip install pylzma pycrypto
WORKDIR /workdir
ENTRYPOINT ["python", "/dedrm/src/k4mobidedrm.py"]
