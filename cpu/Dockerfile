FROM python:3.8-slim AS cirq_base

ENV CIRQ_VERSION 0.11.0
ENV TENSORFLOW_VERSION 2.4.1
ENV TENSORFLOW_QUANTUM_VERSION 0.5.1

# Install dependencies.
# rm -rf /var/lib/apt/lists/* cleans up apt cache. See https://docs.docker.com/develop/develop-images/dockerfile_best-practices/
RUN DEBIAN_FRONTEND=noninteractive apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
     python3-pip \
     locales \
     graphviz \
     && rm -rf /var/lib/apt/lists/*

# Configure UTF-8 encoding.
RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && locale-gen
ENV LANG en_US.UTF-8  
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8 

# Make python3 default
RUN rm -f /usr/bin/python \
     && ln -s /usr/bin/python3 /usr/bin/python
#cirq stable image
FROM cirq_base AS cirq_stable
RUN pip3 install cirq==$CIRQ_VERSION

# TFQ
RUN pip install tensorflow==$TENSORFLOW_VERSION \
     && pip install tensorflow-quantum==$TENSORFLOW_QUANTUM_VERSION \
     && pip install pydot
