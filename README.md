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
hunched 2d599ad2d19dad48f37434e2ee65e377


