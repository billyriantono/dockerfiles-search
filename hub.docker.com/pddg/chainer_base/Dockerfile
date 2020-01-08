FROM chainer/chainer:v4.5.0-python3

LABEL maintainer="Shoma Kokuryo <s.kokuryo@gmail.com>"

# Declare Project dir
ENV PROJECT_DIR /opt/proj

# Change current directory
WORKDIR ${PROJECT_DIR}

# Install dependencies
RUN pip3 install --no-cache-dir \
        # 2D plotting library
        matplotlib==3.0.2 \
        # To parse excel file
        xlrd==1.1.0 \
        # Easy-to-use data structures and data analysis tools
        pandas==0.23.4 \
        # Progress bar module
        tqdm==4.28.1 \
        # Parallel computing
        joblib==0.13.0 \
        # Parse env file and load them into os.environ
        python-dotenv==0.9.1

