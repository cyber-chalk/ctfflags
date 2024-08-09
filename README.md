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
http://10.13.37.10/ 

secret 3 is in the title tag
