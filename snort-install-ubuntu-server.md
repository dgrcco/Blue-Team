![Snort3](https://www.snort.org/assets/Snort_fulllogo.png)

# SNORT3 INSTALL UBUNTU SERVER

## Official Docs (recommended)
[https://docs.snort.org/start/installation](https://github.com/snort3/snort3/blob/master/doc/user/tutorial.txt)

## Update packages

```
sudo apt update && sudo apt upgrade -y
```

## Install apt packages

```
sudo apt install build-essential cmake pkg-config libpcap-dev libdumbnet-dev libhwloc-dev libluajit-5.1-dev libssl-dev libpcre3-dev zlib1g-dev flex bison -y
```

## Install LibDAQ

```
git clone https://github.com/snort3/libdaq.git

cd libdaq
./bootstrap
./configure
sudo make install
sudo ldconfig
```

## Installing snort

```
git clone https://github.com/snort3/snort3.git
./configure_cmake.sh (or follow the og doc)
cd build
make -j $(nproc)
sudo make install
```


# Install packages from source


## Installing dnet (apt install libdumbnet-dev)

```
git clone https://github.com/dugsong/libdnet.git
cd libdnet/
./configure && make
sudo make install
```

## Installing hwloc 

click on the download page: [https://www.open-mpi.org/projects/hwloc/](https://www.open-mpi.org/projects/hwloc/)
```
wget https://download.open-mpi.org/release/open-mpi/v5.0/openmpi-5.0.8.tar.gz
tar zxvf openmpi-5.0.8.tar.gz
cd openmpi-5.0.8/
./configure && make
sudo make install
```

## Installing Openssl

[https://openssl-library.org/source/](https://openssl-library.org/source/)

```
wget https://github.com/openssl/openssl/releases/download/openssl-3.6.0/openssl-3.6.0.tar.gz
tar zxvf openssl-3.6.0.tar.gz
cd openssl-3.6.0/
./Configure && make
sudo make install
```

## Installing libpcap (can be installed with apt)

[https://www.tcpdump.org/index.html#latest-releases](https://www.tcpdump.org/index.html#latest-releases)

```
wget https://www.tcpdump.org/release/libpcap-1.10.5.tar.xz
tar xvf libpcap-1.10.5.tar.xz
cd libpcap-1.10.5/
./configure && make
sudo make install
```

## Installing pcre

[https://github.com/PCRE2Project/pcre2/releases](https://github.com/PCRE2Project/pcre2/releases)

```
wget https://github.com/PCRE2Project/pcre2/releases/download/pcre2-10.47/pcre2-10.47.tar.gz
tar zxvf pcre2-10.47.tar.gz
cd pcre2-10.47/
./configure && make
sudo make install
```

## Installing pkgconfig

[https://www.freedesktop.org/wiki/Software/pkg-config/](https://www.freedesktop.org/wiki/Software/pkg-config/)

```
wget http://pkgconfig.freedesktop.org/releases/pkg-config-0.29.2.tar.gz
tar zxvf pkg-config-0.29.2.tar.gz
cd pkg-config-0.29.2/
./configure && make
sudo make install
```


## Installing pkgconfig (already installed with apt in the first command)

[https://www.freedesktop.org/wiki/Software/pkg-config/](https://www.freedesktop.org/wiki/Software/pkg-config/)

```
wget http://pkgconfig.freedesktop.org/releases/pkg-config-0.29.2.tar.gz
tar zxvf pkg-config-0.29.2.tar.gz
cd pkg-config-0.29.2/
./configure && make
sudo make install
```

## Installing zlib (can be installed with apt)
[https://www.zlib.net/zlib-1.3.1.tar.gz](https://www.zlib.net/zlib-1.3.1.tar.gz)

```
wget https://www.zlib.net/zlib-1.3.1.tar.gz
tar zxvf zlib-1.3.1.tar.gz
cd zlib-1.3.1/
./configure && make
sudo make install
```

# Remove all downloaded files

```
sudo rm -rf *
```




