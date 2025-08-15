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
4. Modify ```nginx.conf``` file at location: ```/usr/local/nginx/conf/nginx.conf``` (for self-compiled) to set up the RTMP server:
```
Refer to the "nginx.conf" file
```
5. HLS web service configuration at location ```/usr/local/nginx/rtmp/html/index.html``` (relative location is ```../rtmp/html/index.html```):
```
Refer to the "index.html" file
```
6. (optional) Enforce authenticated users to watch live streaming:
* Install ```htpasswd``` tool:
```
apt install -y apache2-utils
```
* Create a password file at location ```/usr/local/nginx/rtmp/.htpasswd```:
```
htpasswd -c .htpasswd user_name
```
* To add more users:
```
htpasswd .htpasswd another_user
```
* Ensure nginx can read this ```htpasswd``` file:
```
chown nobody:nogroup .htpasswd  # For compiled Nginx
chmod 640 .htpasswd
```
8. OBS (or other streaming software) configuration:
Check the video is encoded as H.264; For the RTMP server URL and authentication:
```
URL: rtmp://your_domain:port/live
Private key: follow with the HTML setup
```
* Or only with URL (the authentication key is incorporated)
```
URL: rtmp://your_domain:port/live/private_key
```
9. To start the server (or reload): ```nginx``` or ```nginx -s reload```

### Debug:
For the self-compiled nginx server, most files are stored at ```/user/local/nginx/```, which contains:
```
- conf/
-- nginx.conf
-- ...
- logs/
- html/
- rtmp/
-- .htpasswd
-- html/
--- index.html
- ...
```
The temporary video chunks are stored at ```/tmp/hls/```. They will be automatically cleared by nginx.

