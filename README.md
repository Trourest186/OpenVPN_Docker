# OpenVPN_Docker

## Create and initialize openvpn (create openvpn config)
```
docker run --rm -v $PWD:/etc/openvpn kylemanna/openvpn ovpn_genconfig -u udp://<your IP address):1194
```
## Create certificate
```
docker run --rm -v $PWD:/etc/openvpn -it kylemanna/openvpn ovpn_initpki
```
## Create client account

```
docker run --rm -v $PWD:/etc/openvpn -it kylemanna/openvpn easyrsa build-client-full client
```
## Copy client certificate (ovpn file) from container
```
docker run --rm -v $PWD:/etc/openvpn kylemanna/openvpn ovpn_getclient client > client.ovpn
```
## Start OpenVPN container
```
docker run --name openvpn -v $PWD:/etc/openvpn -d -p 1194:1194/udp --cap-add=NET_ADMIN --restart always kylemanna/openvpn
```

## Setup for OpenVPN client (Ex: Linux, Windoex)
- Case for Windows
  https://swupdate.openvpn.org/community/releases/openvpn-install-2.4.6-I602.exe

  Then, edit file with comment out "redirect-gateway def1"
  
  Add rules for routinng (Ex: push "route 172.19.0.0 255.255.255.0")


Other commands
-----------------
Check if container is running: docker ps
Check container logs: docker logs openvpn

