FROM python:3.6-slim

# Update the repositories
RUN apt-get update

# Install graphviz for matplotlib
RUN apt-get install -y graphviz

# Copy the requirements
COPY requirements.txt /req/requirements.txt

# Upgrade pip and install the requirements
RUN pip install --upgrade pip; \
    pip install -r /req/requirements.txt

# Copy the Jupyter configuration
COPY jupyter_notebook_config.py /conf/config.py

# Define the username
ARG USERNAME=data-mining

# Set the HOME environment variable
# to know the path to the user home
ENV HOME /home/$USERNAME

# Add the user
RUN useradd -ms /bin/bash $USERNAME
USER $USERNAME
RUN mkdir -p $HOME/workspace
WORKDIR $HOME/workspace

# Expose the port
EXPOSE 8888

# Run JupyterLab (with the specified configuration)
CMD ["jupyter", "lab", "--config", "/conf/config.py"]
