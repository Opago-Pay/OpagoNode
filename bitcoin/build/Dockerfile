FROM bitnami/minideb:latest
RUN install_packages wget ca-certificates net-tools
RUN cd /tmp
RUN wget https://bitcoincore.org/bin/bitcoin-core-23.0/bitcoin-23.0-x86_64-linux-gnu.tar.gz
RUN tar -xvf bitcoin-23.0-x86_64-linux-gnu.tar.gz
RUN install -m 0755 -o root -g root -t /usr/local/bin bitcoin-23.0/bin/*
RUN mkdir /data
RUN mkdir /data/bitcoin
COPY ./bitcoin.conf /data/bitcoin/bitcoin.conf
RUN chown root:root /data/bitcoin/bitcoin.conf
ENTRYPOINT bitcoind
