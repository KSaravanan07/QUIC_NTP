# QUIC_NTP

A python attack script built on top of aioquic to perform request forgery with QUIC.
MON_List attack for CMRF and DNS query forgery with VNRF

## Prerequisites

- Python3 (3.8)
- NetfilterQueue and ScaPY
- Aioquic (0.9.20)
	1. Pull aioquic 
	2. Checkout a compatible version
	3. Apply the aioquic.diff
	4. Follow the install instructions of aioquic
- Wireshark

## Installation / Setup

If the prerequisites are met the script should run out of the box. The described installation instructions are likely going to change in the future. If the setup instructions fail, please consult the official documentation of the respective software.

### Install NetfilterQueue and ScaPY

```bash
sudo apt install build-essential python-dev libnetfilter-queue-dev
sudo pip install https://github.com/johnteslade/python-netfilterqueue/archive/refs/heads/update-cython-code.zip
sudo pip install scapy 
```

### Installation of aioquic

- Install dependencies
```bash
sudo apt-get update && sudo apt-get install -y git-core libssl-dev python3-dev python3-pip
sudo pip3 install aiofiles asgiref httpbin starlette wsproto werkzeug==2.0.3
```
- Clone the repository
```bash
	git clone https://github.com/aiortc/aioquic && cd /aioquic && git checkout tags/0.9.20
```

- Apply the diff by copying aioquic.diff from QUIC_NTP folder and pasting it in aioquic install location. Then run the following command:
```bash
git apply aioquic.diff
```

## Usage

### Generate Certificates

You can generate your own certificates but they must use the same name as the certificates and keys we have provided as they are hardocoded in the code

### Use the server docker containers
- First Pull the docker container
```bash
sudo docker pull yukonsec/neqo
```
- Run from inside QUIC_NTP folder
```bash
sudo docker run -p 12345:12345/udp -v $PWD/certs:/mnt/certs/ -v $PWD/certs:/mnt/keys -it --rm yukonsec/neqo
```
Here - $PWD is there to refer to current folder from which this is being run. You can replace with absolute path incase of problems.



### Use the attack script
More information about the attack script can be viewed with:

```bash
sudo python3 request_forgery.py -h
```


