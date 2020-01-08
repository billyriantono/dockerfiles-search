FROM challisa/tessmix-opencv:latest

# Expose the ports available for Jupyter
EXPOSE 8888

# Install Python packages defined in requirements.txt
ADD requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt && \
	rm -f requirements.txt && \
# Install any other useful packages
	apt-get update && apt-get install -y \
	vim && \
	rm -rf /var/lib/apt/lists/* && \
  apt-get clean && \
	jupyter contrib nbextension install --system && \
	mkdir /opt/working

WORKDIR "/opt/working"
