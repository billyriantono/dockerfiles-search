ARG CODE_VERSION=develop

# Use the suningdocker/py-rpc runtime as the parent image with CODE_VERSION
FROM suningdocker/py_rpc:${CODE_VERSION}

# Copy python_container_conda_deps.txt file into /lib/, all dependencies needed to be installed is included in python_container_conda_deps.txt
COPY suningclipper_admin/suningclipper_admin/python_container_conda_deps.txt /lib/

# Install any needed packages specified in python_container_conda_deps.txt
RUN conda install -y --file /lib/python_container_conda_deps.txt

# Copy containers/python/python_closure_container.py and containers/python/python_closure_container_entry.sh into /container/
COPY containers/python/python_closure_container.py containers/python/python_closure_container_entry.sh /container/

# Copy all files in suningclipper_admin/ to /lib/suningclipper_admin
COPY suningclipper_admin/ /lib/suningclipper_admin

# Install with pip suningclipper_admin
RUN pip install /lib/suningclipper_admin

# Run /container/python_closure_container_entry.sh when the container launches
CMD ["/container/python_closure_container_entry.sh"]