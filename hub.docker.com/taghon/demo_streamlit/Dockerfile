FROM python:3.7
EXPOSE 8501
RUN pip3 install streamlit
RUN mkdir -p /root/.streamlit/
COPY config.toml /root/.streamlit/
CMD streamlit hello
