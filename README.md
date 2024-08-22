# Capture The Flag (CTF) Challenges


 **I love cat. I love every kind of cat:**
   ```bash
   ls
   cat secret.flag
   # Flag: 8d484567839bed610fc06f21f27ea5f4
   ```

 **Reveal Hidden Attributes:**
   ```bash
   ls -a
   cat .secret.flag
   # Flag: e2d231f3b6142538877c08d01ef2aca1
   ```

 **Navigating Around:**
   ```bash
   ls -la
   cd inhere/
   ls
   cat secret.flag
   # Flag: 5ac6dbc5f21c04325afd5051c1033eb3
   ```


 **Why did the file go to the police?:**
   ```bash
   ls -la
   cd inhere0/
   ls -la
   file ./*
   cat flag06
   # Flag: 355c077b9cc5cc578b0af34cb7ca6153
   ```


 **Why did the computer file feel lost?:**
   ```bash
   ls -la
   find ./ -name "*.flag"
   cat ./inhere3/file35.flag
   # Flag: d50ebc863697dc03a34c5b19ce7c2b08
   ```

**What is in a name?**
   ```bash
   ls -la
   find ./ -user adam
   cat ./inhere6/file65.flag
   # Flag: 2171934626d97652b9dd79caf97a1694
   ```

**Does size count?**
   ```bash
   find ./ -user adam -size 33c
   cat ./inhere6/fjEkweorWp
   # Flag: cda2b8470407afa9f957d02671a58de9
   ```


 **That's a lot of words!:**
  ```bash
  cat os.revision.007.flag | grep hornstone
  # Output: 75b7f8e0279151b85d31ca258b4a7f06
  ```

 **What the wget?:**
  ```bash
  # On local machine
  ls -la
  cat secret.hint
  find / -name "*.7z" 2>/dev/null
  # On remote machine
  wget http://10.13.37.10/secret.flag.7z
  7za x secret.flag.7z
  # Output: a690b51cf7fa8ebaa7f733a334648e20
  ```

 **It is the strings that matter most!:**
  ```bash
  ls -la
  cat secret.hint
  strings secret
  # Output: ./secret 6fa1b41f5a40b34ca707c6d36a231d79
  # CTF Flag: ae87a47a1b8a6eb58843ce6967ab201f
  ```
## NETWORK ADMINISTRATION

### **Hello Containerlabs**


  ```bash
  #On Local Machine
  mkdir hello && cd $_ 
  vim hello.yml
  ```

  **Topology File (`hello.yml`):**
  ```yaml
  name: reverse_ctf_tester
  topology:
    nodes:
      alpine:
        kind: linux
        image: reverse-ctf-server
        ports:
          - "2222:22/tcp"
  ```

  **Deploy and Run:**
  ```bash
  sudo containerlab deploy -t hello.yml  # on remote machine
  ip a
  ./reverse-ctf.sh 10.13.37.55
  ```

  **Flag:**
  ```
  ae87a47a1b8a6eb58843ce6967ab201f
  ```

---

### **Connect Test-Server to a Router**
[guide](https://github.com/carteras/cookbook/blob/main/networks/containerlabs/cookbooks/containerlab.basics.test-to-router.md) 
</br>

![image](https://github.com/user-attachments/assets/b5d4f481-32f6-40c5-b141-1f3bcbeae7fd)

 **Create directory**
  ```bash
  mkdir r1 && cd $_ # On Local Machine
  ```

  **Create Topology File (`idk.yml`):**
  ```yaml
  name: test-router-static
  topology:
    nodes:
      r1:
        kind: linux
        image: frrouting/frr:latest
      test: 
        kind: linux
        image: reverse-ctf-server
        ports:
          - "2222:22/tcp"
    links: 
      - endpoints: ['r1:eth1', 'test:eth1']
  ```

  **Deploy and Configure:**
  ```bash
  sudo containerlab deploy -t idk.yml
  ```

- **R1 Configuration:**
  ```bash
  docker exec -it clab-test-router-static-r1 vtysh
  configure terminal
  interface eth1
  ip address 10.0.0.1/24
  end
  write memory
  show interface brief
  ```

- **Test Server Configuration:**
  ```bash
  docker exec -it clab-test-router-statc-test sh
  apk update
  apk add iproute2
  ip addr add 10.0.0.50/24 dev eth1 
  ip link set eth1 up
  ip route add default via 10.0.0.1
  ./reverse-ctf.sh 10.13.37.55
  ```

  **Flag:**
  ```
  f1223c77990ca35199cb998259d7358a
  ```

---

### **Two Networks, One Router 🤨**
[Two Networks, One Router Guide](https://github.com/carteras/cookbook/blob/main/networks/containerlabs/cookbooks/containerlab.static.router-to-1pc.md)  
<img style="width: 50vw" src="https://github.com/carteras/cookbook/raw/main/networks/containerlabs/cookbooks/image.png" alt="alt text"/>

- **Clean Up Existing Instances:**
  ```bash
  sudo containerlab destroy -a
  ```

- **create dir:**
  ```bash
  mkdir r2 && cd $_ # on local machine
  ```

 add stuff

  **Flag:**
  ```
  937fa2856b905a26fc4e1ed17233f9fb
  ```




## Challenges

### Challenge 000 000
- **Flag:** 03b0cfc0e6a42c09c567184990aeaa9c
  ``` bash
  ls -la
  cat .secret
  ```
  - *Note:* Look for hidden files.

### Challenge 000 001
- **Flag:** 0a5f5a226877af1941a1dcbba1c2af2a
  ```bash
  find / -type f -size +49c -size -61c -exec file {} \; 2>/dev/null | grep 'ASCII text' | grep 'flag'
  ```

### Challenge 000 002
- **Flag:** 2d599ad2d19dad48f37434e2ee65e377
  ```bash
  cat secret.flag | grep -i "^hunched " --ignore-case
  # or
  cat secret.flag | grep hunched -w
  ```

### Challenge 000 003
- **Flag:** 9dd368744a1f1c09753e435434d51326
  - *Note:* Use any previous configuration.
    ```bash
    sudo containerlab deploy -t topology.yml
    ./reverse-ctf.sh 10.13.37.55 # on remote machine
    ``` 

### Challenge 000 004
- **Flag:** bdbd9e2b898a31807eefbdbf1137b66f
  - Follow this guide: [ContainerLab Basics](https://github.com/carteras/cookbook/blob/main/networks/containerlabs/cookbooks/containerlab.basics.test-to-router.md)
  - Resolve routing issues:
    ```bash
    ip route del default via 172.20.20.1 dev eth0
    ip route add default via 10.0.0.1 dev eth1 metric 100
    ip route add default via 172.20.20.1 dev eth0 metric 200
    ```

### Challenge 5
<img style="width: 55vw" src="https://github.com/user-attachments/assets/2fb6ddd8-7899-4f16-8b23-9c7d05174654" alt="staticly routed network"/>

- **Flag:** 027eac9a94926df213c3bf01c9b71832
  - **Setup:**
    ```yaml
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
    ```

  - **Deploy and Configure:**
    ```bash
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

    sudo docker exec -it clab-test-router-static-reverse-ctf sh
    apk update
    apk add iproute2
    ip addr add 10.0.0.10/24 dev eth1
    ip link set eth1 up
    ip route add default via 10.0.0.1 dev eth1 metric 100
    ip route add default via 172.20.20.1 dev eth0 metric 200

    # do this for workstation 1 & 2 (make sure to account for ip addresses)
    ```

### Secret 2
- **Flag:** 2ce7e1ecd7c927681fe302f1e4bd3371
  - URL: [http://10.13.37.10/](http://10.13.37.10/)

### Secret 3
- **Flag:** e6426f62f9cefe09140847daebc55205
  - Found in the `<title>` tag.

### Secret 4
- **Flag:** 027eac9a94926df213c3bf01c9b71832
  - Command: `cd .-`

### Secret 5
- **Flag:** 04b9bb628c11dba362116871829199db
  - Found at: `/etc/conf.d/secret_config/.secret.flag`

### Secret 1
- **Hint for Week 2:** No sudo access to run Docker.

## Additional Resources

- **ContainerLab Guides:**
  - [Test to Router](https://github.com/carteras/cookbook/blob/main/networks/containerlabs/cookbooks/containerlab.basics.test-to-router.md)
  - [Static Router to PC](https://github.com/carteras/cookbook/blob/main/networks/containerlabs/cookbooks/containerlab.static.router-to-1pc.md)

