FROM python:3

RUN pip install numpy pandas matplotlib jupyter

VOLUME ["/source"]
WORKDIR /source
CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root"]
