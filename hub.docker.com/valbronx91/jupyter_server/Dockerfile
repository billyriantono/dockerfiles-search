FROM jupyter/base-notebook:latest 
RUN python3 -m pip install --upgrade pip
RUN pip3 install pandas scikit-learn seaborn numpy lightgbm
USER root
RUN apt-get install openssl
RUN openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout "cert.key" -out "cert.pem" -batch

CMD jupyter notebook --notebook-dir="work" --ip='*' --NotebookApp.token='' --NotebookApp.password='sha1:96f622d5c6fb:e2589395cd4fa53062aa3794da7e770e00934526' --no-browser --port=443 --allow-root --certfile=cert.pem --keyfile cert.key
