# Nginx-based-live-stream-server-tutorial-note
An RTMP server that provides HLS live stream service through nginx and the corresponding module.

<img width="600" height="400" alt="output" src="https://github.com/user-attachments/assets/a6242b13-ec28-4def-9762-0085873aaa9f"/>

### Basic Concepts:

* RTMP protocol
* HLS

### Startup:

1. Install prerequisites:
```
apt update
apt install -y build-essential libpcre3 libpcre3-dev libssl-dev zlib1g-dev wget
```
2. Download nginx and RTMP module (necessary step, since the RTMP module is not included in the default nginx package):
```
wget http://nginx.org/download/nginx-1.24.0.tar.gz
wget https://github.com/arut/nginx-rtmp-module/archive/master.tar.gz
tar -zxvf nginx-1.24.0.tar.gz
tar -zxvf master.tar.gz
```
3. Compile nginx (enter the unzipped nginx folder first):
```
cd nginx-1.24.0
./configure --with-http_ssl_module --add-module=../nginx-rtmp-module-master
make
make install
```
4. Modify ```nginx.conf``` file to set up the RTMP server:
```
Refer to the "nginx.conf" file
```
5. 
