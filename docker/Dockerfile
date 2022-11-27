FROM --platform=linux/amd64 ubuntu:20.04

LABEL maintainer="ldfandian@hotmail.com"
LABEL version="0.1.0"

# change to use China sources
RUN sed -i 's/archive.ubuntu.com/mirrors.aliyun.com/' /etc/apt/sources.list \
 && sed -i 's/security.ubuntu.com/mirrors.aliyun.com/' /etc/apt/sources.list 

# basic os management tools
ENV LANGUAGE=en_US.UTF-8
ENV LANG=en_US.UTF-8
ENV LC_ALL=C
RUN apt-get update -y \
  && apt-get install -y apt-utils \
  && apt-get install -y iproute2 procps lsb-release build-essential net-tools iputils-ping file psmisc \
  && apt-get install -y vim wget curl tree jshon

# install basic dev tools
RUN apt-get install -y g++ gcc make autoconf automake

# install python 3.10
RUN DEBIAN_FRONTEND=noninteractive TZ=Asia/Shanghai apt-get install -y software-properties-common
RUN add-apt-repository ppa:deadsnakes/ppa && apt-get update -y
RUN apt-get remove -y python3 python3-pip && apt-get autoremove -y
RUN DEBIAN_FRONTEND=noninteractive TZ=Asia/Shanghai apt-get install -y python3.10
RUN ln -s /usr/bin/python3.10 /usr/bin/python3 && ln -s /usr/bin/python3.10 /usr/bin/python
RUN apt-get install -y python3.10-distutils
RUN curl https://bootstrap.pypa.io/get-pip.py -o /tmp/get-pip.py \
  && python3 /tmp/get-pip.py && python3 /tmp/get-pip.py --user && rm -f /tmp/get-pip.py

# install ffmpeg (for the latest filter)
RUN DEBIAN_FRONTEND=noninteractive TZ=Asia/Shanghai apt-get install -y ffmpeg

#  && add-apt-repository -y ppa:savoury1/ffmpeg4 && apt-get -y update && apt-get install -y ffmpeg

# setup whisper
RUN apt-get install -y git
RUN pip3 config set global.index-url https://mirrors.aliyun.com/pypi/simple --user && pip3 config set install.trusted-host mirrors.aliyun.com --user
RUN pip install setuptools-rust
RUN pip install git+https://github.com/openai/whisper.git 
RUN pip install --upgrade --no-deps --force-reinstall git+https://github.com/openai/whisper.git
# RUN pip uninstall -y torch && pip cache purge && pip install torch -f https://download.pytorch.org/whl/torch_stable.html

# set working directory 
WORKDIR /mnt/devroot/openai-whisper/

# starting app
CMD [ "/bin/bash" ]

