FROM ubuntu:16.04
MAINTAINER Y2Kot

RUN \
  sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
  apt-get update && \
  apt-get -y upgrade && \
  apt-get install -y software-properties-common

RUN add-apt-repository -y ppa:myriadrf/drivers
RUN apt-get update
RUN apt-get install -y cmake g++ libpython-dev python-numpy swig \
		git g++ cmake libsqlite3-dev libsoapysdr-dev libi2c-dev \
		libusb-1.0-0-dev libwxgtk3.0-dev freeglut3-dev \
		libboost-all-dev python-mako doxygen python-docutils \
		build-essential

WORKDIR /home/base
RUN git clone https://github.com/pothosware/SoapySDR.git
RUN git clone https://github.com/myriadrf/LimeSuite.git
RUN git clone git://github.com/EttusResearch/uhd.git
RUN git clone https://github.com/pothosware/SoapyUHD

WORKDIR /home/base/SoapySDR/build
RUN cmake ../ && make -j4 && make install && ldconfig

WORKDIR /home/base/LimeSuite/builddir
RUN cmake ../ && make -j4 && make install && ldconfig

WORKDIR /home/base/uhd/host/build
RUN cmake ../ && make -j4 && make install && ldconfig

WORKDIR /home/base/SoapyUHD/build
RUN cmake ../ && make -j4 && make install && ldconfig

WORKDIR /home
RUN rm -rf base
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

CMD ["bash"]
