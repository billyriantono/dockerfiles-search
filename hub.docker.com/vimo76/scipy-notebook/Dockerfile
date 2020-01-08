FROM jupyter/scipy-notebook

# Upgrade outdated pandas package that's installed with scipy-notebook
RUN pip install --upgrade pip & \
    pip install --upgrade pandas

# Change workdir to work
WORKDIR /home/$NB_USER/work