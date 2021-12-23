# Remote SSH
Setting up a remote ssh is going to be super easy and you should use it at all times since the terminal from virtual box is just utter shit.

## Setting up UFW

First install UFW:
```bash
sudo apt-get install ufw
```

Next we need to open a port using ufw, a port in laymans terms is basically a door to which stuff can go through. So imagine trying to connect from our host machine to our virtual one. The virtual machine needs to have a door open to ssh through for our host, else the host can't create a sucessfull connection.

## Handeling ports and port forwarding

First enable UFW:
```bash
sudo ufw enable
```

Here are some general commands for UFW:

### Checking for our ports
```bash
sudo ufw status
```

### Opening a port
```bash
sudo ufw allow 4242
```

### Deleting a port
Use ```sudo ufw status numbered``` to get the index.
```bash
sudo ufw delete <index>
```

Last but not least we need to do some port forwarding aka redirect our host's port to our guest port. That way when we ssh to our machines port 4242 we get re-directed to the guest's port 4242 which we luckily opened for our host!

To do this go to ```Settings > Network > Advanced > Port Forwarding```
![port](/images/port.png)

Click on the green ```+``` icon and just do what I did here, yup thats it.

![port](/images/port2.png)

## There shall be a connection!

Now go do ```cd /etc/ssh``` and edit the ```sshd_config``` file with sudo!

Find the line that says ```#Port <number>``` uncomment it and change it to 4242.
![config](/images/ssh_config.png)


Now go to your host machine, and login via:
```bash
ssh <username>@localhost -p 4242
```
