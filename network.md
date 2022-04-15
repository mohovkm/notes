### find port in use (3306) and kill it
```bash
sudo fuser 3306/tcp
# 3306/tcp:            651510
sudo kill -9 651510
```

### Find ip addres that belongs to the DNS name:
```bash
nslookup https://address_to_find.com
``` 

### Find out if port opened or not
```bash
nc -zvn 127.0.0.1 443
```

### Create tunnel to be able to reach IP via port:
#### https://www.tecmint.com/create-ssh-tunneling-port-forwarding-in-linux/
```bash
ssh remote_ip -l username -L 8443:another_remote_ip:8443
ssh 129.168.1.1 -l mohovkm -L 8443:192.168.1.2:8443
```

### More about tunneling
You can forward a local port (e.g 8080) which you can then use to access the application locally as follows. The `-L` flag defines the port forwarded to the remote host and remote port.

```bash
ssh admin@server1.example.com -L 8080:server1.example.com:3000
```
Adding the `-N` flag means do not execute a remote command, you will not get a shell in this case.

```bash
ssh -N admin@server1.example.com -L 8080:server1.example.com:3000
```
The `-f` switch instructs ssh to run in the background.

```bash
ssh -f -N admin@server1.example.com -L 8080:server1.example.com:3000
```
Now, on your local machine, open a browser, instead of accessing the remote application using the address server1.example.com:3000, you can simply use `localhost:8080`

### Copy public id
1. list your public keys
```bash
ls ~/.ssh/id*
```

2. Copy default (or needed) public key
```bash
ssh-copy-id user@remote-host
# or
ssh-copy-id -i ~/.ssh/other_key.pub user@remote-host
```

3. Copy key from another user
```bash
kmokhov@server1$ scp /home/another_user/.ssh/id_rsa.pub server_ip:/home/another_user/.ssh/authorized_keys
```
