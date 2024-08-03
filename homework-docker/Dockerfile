FROM nvidia/cuda:12.2.0-runtime-ubuntu22.04

ARG JUPYTER_LAB_PORT
ENV JUPYTER_LAB_PORT ${JUPYTER_LAB_PORT}
ENV DEBIAN_FRONTEND=noninteractive LANG=C TZ=UTC
ENV TERM linux

# install some basic utilities
RUN set -xue ;\
    apt-get update ;\
    apt-get install -y --no-install-recommends \
        build-essential \
        libsm6 \
        libxext6 \
        libxrender-dev \
        libglib2.0-0 \
        wget \
        python3-dev \
        python3-pip \
    ;\
    rm -rf /var/lib/apt/lists/*

# Upgrage pip separately
RUN pip3 install --upgrade pip

# Install all requirements
WORKDIR /playground
COPY requirements.txt ./requirements.txt
RUN pip3 install -r requirements.txt


# Expose port to get access via host
EXPOSE 8088

# Run jupyter lab
CMD jupyter lab --port=${JUPYTER_LAB_PORT} --no-browser --ip=0.0.0.0 --allow-root