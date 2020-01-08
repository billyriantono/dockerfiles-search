FROM continuumio/miniconda3:4.3.14

MAINTAINER Anthony Ebert <anthonyebert@gmail.com>

# Install debian things
RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y x11-apps r-base

# Install NumPy / Matplotlib / Jupyter.
RUN /opt/conda/bin/conda install numpy matplotlib jupyter -y --quiet

# Install libzmq
RUN apt-get update \
    && apt-get upgrade -y -o Dpkg::Options::="--force-confdef" -o DPkg::Options::="--force-confold" \
    && apt-get install -y \
    libzmq3-dev \
    libzmq3

# Add user
RUN adduser user --gecos "First Last,RoomNumber,WorkPhone,HomePhone" --disabled-password

RUN echo "user:user" | chpasswd



# Install Julia0.6.0
RUN mkdir -p /opt/julia-0.6.0 && \
    curl -s -L https://julialang.s3.amazonaws.com/bin/linux/x64/0.6/julia-0.6.0-linux-x86_64.tar.gz | tar -C /opt/julia-0.6.0 -x -z --strip-components=1 -f -
RUN ln -fs /opt/julia-0.6.0 /opt/julia-0.6

# Make v0.6.0 default julia
RUN ln -fs /opt/julia-0.6.0 /opt/julia

# RUN echo "PATH=\"/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/opt/julia/bin\"" > /etc/environment && \
#     echo "export PATH" >> /etc/environment && \
#     echo "source /etc/environment" >> /root/.bashrc

ENV PATH /opt/julia/bin:$PATH

# Install IJulia with using installed miniconda, and then precompile it
RUN CONDA_JL_HOME=/opt/conda /opt/julia/bin/julia -e 'Pkg.add("IJulia");Pkg.build("IJulia");using IJulia'

# Install PyPlot with using installed matplotlib, and then precompile it
RUN PYTHON=/opt/conda/bin/python /opt/julia/bin/julia -e 'Pkg.add("PyPlot");using PyPlot'

# Dependencies for ACEMS workshop
# RUN julia -e 'Pkg.update(); Pkg.update(); Pkg.add("DataFrames"); Pkg.add("DataStructures"); Pkg.add("Distributions"); Pkg.add("JSON"); Pkg.add("Iterators")'



# Define working directory.
WORKDIR /opt/notebooks

# EXPOSE
EXPOSE 8888

# Define default command.
# CMD ["/opt/conda/bin/jupyter", "notebook", "--notebook-dir=/opt/notebooks", "--ip='*'", "--port=8888", "--no-browser"]
CMD ["/bin/bash"]




