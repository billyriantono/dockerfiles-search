FROM debian

# Make logging/io work w/ Docker.
ENV PYTHONUNBUFFERED=1


# Get basic Python dependencies.
RUN apt update && apt upgrade -y && \
  apt install python3-pip curl nano -y && \
  pip3 install pandas numpy && \
  pip3 install -i https://test.pypi.org/simple/ lambdata-elisabethdawn && \
  python3 -c "import lambdata_elisabethdawn; print('Success!')"
