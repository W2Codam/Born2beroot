# Monitoring Script

So, you're trying to go through shell hell? Great! Cause you will be doing a lot of awk's , grep's and tr's. Have fun!

Whats the point of this annoying popup? Well 42 just thought you had to revisit shell00 and shell01 from the piscine :D

---

## Setup

To start off go to your ```/etc/``` directory and run ```touch monitoring.sh``` in that directory.

Why that directory ? Because thats the point of **/etc/** it contains miscellaneous files regarding the machine. Surely you can put it wherever but its good practice to understand where goes what and what goes where.

Next use whatever editor you want to use, in this example I will use ```Nano``` because fuck vim.

As described by the subject every 10 minutes, checkout [crontab](../crontab/index.md) for that, we need to run this script and display something along the lines of:

![Yuck](/images/Monitoring.png)

### First step

Every shell script needs a "*shebang*" aka informing which interpreter to use when
running the script. Setup your script like this:

```bash
#!/bin/bash

#Variables

#Output
wall "

"
```

### Here's the entrance to hell.

SO now that we got our file lets write this mess.

First we need to display our architecture which basically just describes what we are using, aka what version of linux, distro, cpu architecture...

```wall``` is whats supposed to be used to display a message to **ALL** connected users, **no**, do not think of creating an echo chain, thats disgusting! 

```bash
#!/bin/bash

#Variables
ARCH=`uname -a`

#Output
wall "
Architecture: $ARCH
"
```

This process will be repeated constantly, we execute a shell command, store its output in a variable and reference it later in ```wall``` to output.

There's a few edge cases however that need to be taken into account! The rest is pretty much up to you to figure out, its really just googling most things.

---

### CPU Physical/Virtual proccesors!

My approach of getting the CPU physical & virtual processors might be utterly wrong, I honestly have not found anyone who was able to tell me the right way and I only managed to find the answer via google which gave me the "correct" amount which will usually almost for everyone be 1.

Basically for each new processor a line is added, the number indicates the index. So even if it says 0 withouth the ```wc -l``` command, its correct as its just the index.

### Disk Usage!

When getting the disk usage via ```df``` any and **ALL** ```tmpfs``` should not be taken into account for calculating the disk usage. Why ? Because they are temp! Basically linux does not allocate actual disk space for them, they purely exist as virtual files in memory. Which to no surprise at all gets wiped every boot, such is the nature of temp.

---

## Result

No, do not copy paste this if you don't understand it!

*I know you will you lazy programmer!*

![Yuck2](/images/Monitor.png)
