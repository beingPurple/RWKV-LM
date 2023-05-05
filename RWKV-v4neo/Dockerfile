FROM ubuntu:20.04
LABEL maintainer="ppg0291@gmail.com"
RUN apt-get -y update && apt-get -y upgrade && \
    apt-get -y install wget && \
    apt-get -y install nginx && \
    rm -rf /var/lib/apt/lists/*

# Install Anaconda
 RUN wget https://repo.anaconda.com/archive/Anaconda3-2023.03-Linux-x86_64.sh && \
    RUN bash Anaconda3-2023.03-Linux-x86_64.sh -b -p /opt/anaconda3 && \
    # rm Anaconda3-2023.03-Linux-x86_64.sh

ENV PATH="/opt/anaconda3/bin:${PATH}"

# Install DeepSpeed with CPU_ADAM
 RUN git clone https://github.com/microsoft/DeepSpeed.git && \
    RUN cd deepSpeed && \
    DS_BUILD_CPU_ADAM=1 pip install -e . && \
    cd ..

# Copy the requirements.txt file and install the required packages
COPY requirements.txt /app/
COPY torch-1.13.1+cu117.with.pypi.cudnn-cp310-cp310-linux_x86_64.whl /app/
WORKDIR /app
RUN pip install -r requirements.txt

EXPOSE 80

CMD ["/usr/sbin/nginx", "-g", "daemon off;"]
