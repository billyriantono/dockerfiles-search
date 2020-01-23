FROM continuumio/anaconda3

VOLUME /app/notebooks

RUN apt update
RUN apt install nodejs npm -y
RUN npm install -g tslab
RUN tslab install
RUN jupyter labextension install @rahlir/theme-gruvbox


EXPOSE 8888

CMD ["jupyter", "lab", "--ip='0.0.0.0'", "--port=8888", "--no-browser", "--allow-root", "--notebook-dir='/app/notebooks'", "--config='/app/data/config.py'"]