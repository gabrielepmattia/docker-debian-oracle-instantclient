FROM debian:bookworm

RUN apt update && apt upgrade -y && apt install -y libaio1 wget unzip

RUN mkdir /install
WORKDIR /install

RUN wget https://download.oracle.com/otn_software/linux/instantclient/211000/instantclient-basiclite-linux.x64-21.1.0.0.0.zip
RUN wget https://download.oracle.com/otn_software/linux/instantclient/2112000/instantclient-basiclite-linux.x64-21.12.0.0.0dbru.zip

RUN unzip instantclient-basiclite-linux.x64-21.12.0.0.0dbru.zip && \
    mkdir -p /opt/oracle/instantclient_21_12 && \
    mv instantclient_21_12 /opt/oracle/ && \
    echo /opt/oracle/instantclient_21_12 > /etc/ld.so.conf.d/oracle-instantclient.conf && \
    ldconfig

    # mkdir -p /opt/oracle/instantclient_21_1/lib && \
    # ln -sfv /opt/oracle/instantclient_21_1/*.so* /opt/oracle/instantclient_21_1/lib/ && \
    # ln -sfv /usr/lib/libc.so /usr/lib/libresolv.so.2 && \
    # ln -sfv /lib/libc.musl-x86_64.so.1 /lib/ld-linux-x86-64.so.2

ENV ORACLE_BASE=/opt/oracle/instantclient_21_12
# ENV LD_LIBRARY_PATH=/opt/oracle/instantclient_21_1:/lib:/usr/lib
ENV TNS_ADMIN=/opt/oracle/instantclient_21_12
ENV ORACLE_HOME=/opt/oracle/instantclient_21_12

RUN rm -rfv /install
RUN apt purge -y wget unzip
WORKDIR /