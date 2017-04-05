
FROM nvidia/cuda:7.5
MAINTAINER christopher.lee.williams@gmail.com

RUN apt-get update && \
    apt-get -y install wget

#https://devtalk.nvidia.com/default/topic/968891/repository-signing-key-change/
RUN wget -qO - http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1404/x86_64/7fa2af80.pub | sudo apt-key add -

RUN apt-get update && \
    apt-get -y install cuda-visual-tools-7-5 \
    pkg-config \
    openslide-tools \
    libopenslide-dev \
    cmake\
    qt5-default\
    unzip \
    libjpeg-dev \
    libpng-dev \
    libtiff-dev \
    libboost-all-dev \
    libglib2.0-dev


#ADD run /usr/local/cuda-7.5/bin/nsight

#https://github.com/fgrehm/docker-eclipse
RUN chmod +x /usr/local/cuda-7.5/bin/nsight && \
    mkdir -p /home/developer && \
    echo "developer:x:1000:1000:Developer,,,:/home/developer:/bin/bash" >> /etc/passwd && \
    echo "developer:x:1000:" >> /etc/group && \
    echo "developer ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/developer && \
    chmod 0440 /etc/sudoers.d/developer && \
    chown developer:developer -R /home/developer && \
    chown root:root /usr/bin/sudo && chmod 4755 /usr/bin/sudo

    WORKDIR /tmp
    RUN wget https://github.com/Itseez/opencv/archive/2.4.13.zip
    RUN unzip 2.4.13.zip
    RUN mkdir /tmp/opencv-2.4.13/release
    WORKDIR /tmp/opencv-2.4.13/release
    RUN cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D WITH_TBB=ON -D BUILD_NEW_PYTHON_SUPPORT=OFF -D WITH_V4L=ON -D INSTALL_C_EXAMPLES=OFF -D INSTALL_PYTHON_EXAMPLES=OFF -D BUILD_EXAMPLES=OFF -D WITH_QT=ON -D WITH_OPENGL=ON -D ENABLE_FAST_MATH=1 -D CUDA_FAST_MATH=1 -D WITH_CUBLAS=1 -D WITH_CUDA=ON ..
    RUN make
    RUN make install
    WORKDIR /home/developer
    RUN rm /tmp/2.4.13.zip
    RUN rm -R /tmp/opencv-2.4.13

RUN echo "/usr/local/lib" > /etc/ld.so.conf.d/opencv.conf && \
  ldconfig -v

USER developer
ENV HOME /home/developer
WORKDIR /home/developer
#CMD bash
CMD /usr/local/cuda-7.5/bin/nsight
