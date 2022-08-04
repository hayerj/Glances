# Glances
```wrap
 apt install glances 

curl -L https://bit.ly/glances | /bin/bash
```
Web browser 
```wrap
glances -w
https://localhost:61208
```


# Installing Glances auto start
```wrap
 apt update

 apt install python3 -y
```
**After that completes, we'll install pip3 with**
```wrap
apt install python3-pip
```
**Install Glances and Bottle**
```wrap
pip3 install bottle
pip3 install glances
```
```wrap
glances
glances -w
Glances Web User Interface started on http://0.0.0.0:61208/
```

**Create the Glances Service**
```wrap
nano /etc/systemd/system/glances.service
```
**Add**

```wrap
[Unit]
Description = Glances in Web Server Mode
After = network.target

[Service]
ExecStart = /usr/local/bin/glances  -w  -t  5

[Install]
WantedBy = multi-user.target
```
```wrap
which glances
/usr/local/bin/glances or  /home/<your usre>/.local/bin/glances 
```

**We do the following commands to do this**
```wrap
systemctl enable glances.service

systemctl start glances.service

systemctl status glances
```

**Now that it's running, you can again go to the ip address of**
```wrap
http://<local ip>:61208
```

# Adding Widgets to Dashy
```wrap
cd ~/docker/dashy/public
```
```wrap
cp conf.yml conf.bak.yml
```
```wrap
nano conf.yml
```
```wrap
sections:
  - name: Server Info
    widgets:
      - type: gl-current-cpu
        options:
          hostname: http:192.168.10.209:61208
      - type: gl-current-mem
        options:
          hostname: http:192.168.10.209:61208
