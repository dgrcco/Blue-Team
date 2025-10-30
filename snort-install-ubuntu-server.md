# Snort 3 Installation on Ubuntu Server

![Snort3](https://www.snort.org/assets/Snort_fulllogo.png)

## Official Documentation (Recommended)

* [https://docs.snort.org/start/installation](https://docs.snort.org/start/installation)
* [https://github.com/snort3/snort3/blob/master/doc/user/tutorial.txt](https://github.com/snort3/snort3/blob/master/doc/user/tutorial.txt)

---

## 1. Update System Packages

```
sudo apt update && sudo apt upgrade -y
```

---

## 2. Install Required Dependencies

```
sudo apt install -y \
  build-essential cmake pkg-config \
  libpcap-dev libdumbnet-dev libhwloc-dev \
  libluajit-5.1-dev libssl-dev libpcre3-dev \
  zlib1g-dev flex bison
```

---

## 3. Install LibDAQ

```
git clone https://github.com/snort3/libdaq.git
cd libdaq
./bootstrap
./configure
sudo make install
sudo ldconfig
```

---

## 4. Install Snort 3

```
git clone https://github.com/snort3/snort3.git
cd snort3
./configure_cmake.sh
cd build
make -j $(nproc)
sudo make install
sudo ldconfig
```

---

## 5. Add Snort to PATH

```
echo 'export PATH=/usr/local/snort/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```

Verify:

```
snort -V
```

---

## Example Output

```
   ,,_     -*> Snort++ <*-
  o"  )~   Version 3.9.6.0
   ''''    Using DAQ version 3.0.21
```

---

# Extra: Installing Components from Source (Optional)

## libdnet

```
git clone https://github.com/dugsong/libdnet.git
cd libdnet
./configure && make
sudo make install
```

## hwloc

Download: [https://www.open-mpi.org/projects/hwloc/](https://www.open-mpi.org/projects/hwloc/)

```
wget https://download.open-mpi.org/release/open-mpi/v5.0/openmpi-5.0.8.tar.gz
tar zxvf openmpi-5.0.8.tar.gz
cd openmpi-5.0.8
./configure && make
sudo make install
```

## OpenSSL

```
wget https://github.com/openssl/openssl/releases/download/openssl-3.6.0/openssl-3.6.0.tar.gz
tar zxvf openssl-3.6.0.tar.gz
cd openssl-3.6.0
./Configure && make
sudo make install
```

## libpcap

```
wget https://www.tcpdump.org/release/libpcap-1.10.5.tar.xz
tar xvf libpcap-1.10.5.tar.xz
cd libpcap-1.10.5
./configure && make
sudo make install
```

## pcre2

```
wget https://github.com/PCRE2Project/pcre2/releases/download/pcre2-10.47/pcre2-10.47.tar.gz
tar zxvf pcre2-10.47.tar.gz
cd pcre2-10.47
./configure && make
sudo make install
```

## pkgconfig

```
wget http://pkgconfig.freedesktop.org/releases/pkg-config-0.29.2.tar.gz
tar zxvf pkg-config-0.29.2.tar.gz
cd pkg-config-0.29.2
./configure && make
sudo make install
```

## zlib

```
wget https://www.zlib.net/zlib-1.3.1.tar.gz
tar zxvf zlib-1.3.1.tar.gz
cd zlib-1.3.1
./configure && make
sudo make install
```

---

## Clean Download Directory

```
sudo rm -rf *
```
