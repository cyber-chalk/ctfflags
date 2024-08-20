# ctfflags

thats a lot of words:
cat os.revision.007.flag | grep hornstone
75b7f8e0279151b85d31ca258b4a7f06

wget:
cat secret.flag
 find / -name "*.7z" 2>/dev/null
wget 10.13.37.10/secret.flag.7z (password is given in secret.flag)
7za x secret.flag.7z
a690b51cf7fa8ebaa7f733a334648e20

It is the strings that matter most!:
./secret
Usage: ./secret <string>
os_revision009@bushranger:~$ cat secret.hint
Just because it looks like a flag, doesn't mean it is a flag
os_revision009@bushranger:~$ strings secret
./secret 6fa1b41f5a40b34ca707c6d36a231d79
CTF Flag: ae87a47a1b8a6eb58843ce6967ab201f

Hello Containerlabs
vim hello.yml
sudo containerlab deploy -t hello.yml
./reverse-ctf.sh 10.13.37.55
ae87a47a1b8a6eb58843ce6967ab201f


secret 2:
http://10.13.37.10/  2ce7e1ecd7c927681fe302f1e4bd3371

secret 3 is in the title tag 
secret.003 e6426f62f9cefe09140847daebc55205


Connect test-server to a router:
https://github.com/carteras/cookbook/blob/main/networks/containerlabs/cookbooks/containerlab.basics.test-to-router.md 


two networks one router
https://github.com/carteras/cookbook/blob/main/networks/containerlabs/cookbooks/containerlab.static.router-to-1pc.md
937fa2856b905a26fc4e1ed17233f9fb


challenge 0000 000 
03b0cfc0e6a42c09c567184990aeaa9c literally just see hidden file


chgallenge 000110101
0a5f5a226877af1941a1dcbba1c2af2a  
find / -type f -size +49c -size -61c -exec file {} \; 2>/dev/null | grep 'ASCII text' | grep 'flag'
-exec file {} \; runs the file command on each file found.

challenge 01002
cat secret.flag | grep -i "^hunched " --ignore-case
or use -w
hunched 2d599ad2d19dad48f37434e2ee65e377


chal 3
9dd368744a1f1c09753e435434d51326
literally just use any config you used before and put in ip to ./

chal4
bdbd9e2b898a31807eefbdbf1137b66f
follow: https://github.com/carteras/cookbook/blob/main/networks/containerlabs/cookbooks/containerlab.basics.test-to-router.md copy yml as well
you will notice on ip route add default via 10.13.36.1
RTNETLINK answers: File exists
so:
ip route del default via 172.20.20.1 dev eth0
ip route add default via 10.0.0.1 dev eth1 metric 100
ip route add default via 172.20.20.1 dev eth0 metric 200 // not sure if this is neccesary
sudo containerlab inspect -a if you want :)


Chal5
name: test-router-static
topology:
  nodes:
    r1:
      kind: linux
      image: frrouting/frr:latest

    workstation1:
      kind: linux
      image: alpine:latest

    workstation2:
      kind: linux
      image: alpine:latest

    reverse-ctf:
      kind: linux
      image: reverse-ctf-server
      ports:
        - "2222:22/tcp"
  links:
    - endpoints: ['r1:eth1', 'reverse-ctf:eth1']
    - endpoints: ['r1:eth2', 'workstation1:eth1']
    - endpoints: ['r1:eth3', 'workstation2:eth1']
    
sudo containerlab deploy -t five.yml

sudo docker exec -it clab-test-router-static-r1 vtysh
r1# configure terminal
r1(config)# interface eth1
r1(config-if)# ip address 10.0.0.1/24
r1(config-if)# interface eth2
r1(config-if)# ip address 10.13.36.1/24
r1(config-if)# interface eth3
r1(config-if)# ip address 10.10.0.1/24
r1(config-if)# end
write memory
add ip address of eth ip's (inside the box of the router diagram)


sudo docker exec -it clab-test-router-static-reverse-ctf sh
apk update
apk add iproute2
ip addr add 10.0.0.10/24 dev eth1
ip link set eth1 up
 # ip route del default via 172.20.20.1 dev eth0
/ # ip route add default via 10.0.0.1 dev eth1 metric 100
/ # ip route add default via 172.20.20.1 dev eth0 metric 200

exit
set up its eth1
027eac9a94926df213c3bf01c9b71832

secret 4
cd .-
027eac9a94926df213c3bf01c9b71832

secret 5:
 find / -name "*secret*" 2> /dev/null
 file ./* (optional)
 vim /etc/conf.d/secret_config/.secret.flag  (just looked)
04b9bb628c11dba362116871829199db

secret 1:
hint: we did f all in week 2 because adam couldnt get container labs up
also, we didnt have sudo access to run docker in week 2 
