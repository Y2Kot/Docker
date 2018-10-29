FROM y2kot/osmobase
MAINTAINER Y2Kot

RUN \
  sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
  apt-get update && \
  apt-get -y upgrade && \
apt-get install -y software-properties-common

RUN apt-get -y install screen git wget autoconf libtalloc-dev libpcsclite-dev libgnutls-dev \
	libfftw3-dev libortp-dev libsctp-dev libssl-dev libdbi-dev libdbd-sqlite3

WORKDIR /home/osmo
RUN git clone git://git.osmocom.org/libosmocore.git
RUN git clone git://git.osmocom.org/osmo-trx.git
RUN git clone git://git.osmocom.org/libosmo-abis.git
RUN git clone git://git.osmocom.org/libosmo-netif.git
RUN git clone git://git.osmocom.org/openbsc.git
RUN git clone git://git.osmocom.org/osmo-bts.git

WORKDIR /home/osmo/libosmocore
RUN autoreconf -fi && ./configure && make -j4 && make install && ldconfig

WORKDIR /home/osmo/osmo-trx
RUN autoreconf -fi && ./configure --with-lms && make -j4 && make install && ldconfig

WORKDIR /home/osmo/libosmo-abis
RUN autoreconf -fi && ./configure && make -j4 && make install && ldconfig

WORKDIR /home/osmo/libosmo-netif
RUN autoreconf -fi && ./configure && make -j4 && make install && ldconfig

WORKDIR /home/osmo/openbsc/openbsc
RUN autoreconf -fi && ./configure && make -j4 && make install && ldconfig

WORKDIR /home/osmo/osmo-bts
RUN autoreconf -fi && ./configure --enable-trx && make -j4 && make install && ldconfig

WORKDIR /home

#RUN wget https://raw.githubusercontent.com/Y2Kot/Docker/master/OsmoConfigs/openbsc.cfg
RUN wget https://raw.githubusercontent.com/Y2Kot/Docker/master/OsmoConfigs/osmo-trx.cfg
#RUN wget https://raw.githubusercontent.com/Y2Kot/Docker/master/OsmoConfigs/osmo-bts.cfg

COPY startBTS /home/
RUN chmod +x startBTS
RUN rm -rf osmo
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

CMD ["bash"]
