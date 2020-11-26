+++
title= "Jupyterlab on Linux Server"
date= "2020-11-26T16:29:38-05:00"
draft= false
share=true
tags = ['jupyter', 'programming', 'ubuntu']
+++

# Jupyterlab on linux server

- [Overview](#overview)
- [Installation](#anaconda-installation)
- [Virtual environment](#virtual_environment)
- [Issues](#issues)
- [Reference](#reference)

---
## Overview

Jupyterlab is a lightweight but comprehensive and full-development IDE. In addition to write scripts with nice highlights syntax for Python and R as I know, the notebook is probably the most well-known feature with which users are able to write codes along with markdown-style notes. Besides, if you are a user who tends to install as less softwares/packages on your local machine as possible, running Jupyterlab on remote server may be suitable for you. In fact, you don't even install Python or Anaconda in your computer. Let's start to deploy essential tools for your working environment totally on remote machines!

---
## Anaconda installation

One of the easiest and quickest way to setup your working environment with Jupyterlab is to download Jupyterlab in your remote server.

```
mkdir download # If necessary.
# The url could be different depending on the version of anaconda you want.
wget -P /home/download https://repo.anaconda.com/archive/Anaconda3-2019.10-Linux-x86_64.sh
bash /home/download/Anaconda3-2019.10-Linux-x86_64.sh
```

---
## Virtual environment (Optional)

For different projects, you may want to install different packages which could result in the changes for settings. To avoid unwanted troubles, virtual environment becomes useful for isolating development spaces.

Initiating a virtual environment is prettry easy. We could enter the command below in remote server terminal.

```
conda create -n [ENVname] python=3.8 anaconda
```

After installation process, you can now activate your virtual environment by applying the name you used.

```
conda activate [ENVname]
```

From now on, we are ready to install Jupyterlab and any other packages you need.

---
## Install and run Jupyterlab on remote server

With anaconda, package installation becomes very simple. To install Jupyterlab, we just need to use the command below.

```
conda install Jupyterlab
```

Once Jupyterlab has been setup in your remote server, you can start to install SSH tools for remote connections.

### Windows

Although updates for Win10 provides SSH tool accompanying the OS, I will only share my method using an open-source SSH tool [Putty](https://www.putty.org/) because there was no built-in SSH tool inside Windows when I firstly used Linux server. Specifically, we only need to give IP-address, port number, and select `SSH` in the checkbox of the connection type. Once we connect to our remote machine via Putty (entering your password if needed), we should be able to initialize Jupyterlab in the remote server.

```
(server)$ jupyter notebook --no-browser --port=9000 
```
The suffix with `--port=9000` must match the port you use in your local machine. Usually, I activate a command terminal in my local Windows machine and enter
```
(greatlakes) $ ssh -N -f -L localhost:8888:localhost:9000 -p 22 username@greatlakes.arc-ts.umich.edu 
```
Again, the port 8888 is like a hand from our local machine holding hand, the port 9000, extended from server.

### Linux

If you are running an Linux distribution OS, we just need to install SSH server which does not install by default.

```
sudo apt update
sudo apt install openssh-server
```

Once the installation is completed, it is recommended that checking the SSH status by `sudo systemctl status ssh` should report `Active: active (running)` as an output.

Considering the firewall that could block connections, we could apply the command.

```
sudo ufw allow ssh
```

Next, in my case, I need to connect my local machine to the greatlakes server belonging to UM. Therefore, only `username@ip_address` is required for SSH.

```
ssh username@greatlakes.arc-ts.umich.edu
```

Please don't hack into my account anyway lol.

In case you have no idea about the ip address of your server, you can enter `ip a` for getting the required information.

After running the command above, we should see a message to let you enter your password and any other identity verification.

### Initiate Jupyterlab in remote server

While we'd like to run all the programs and Jupyterlab in remote server, we still want to use the IDE in our local machine. Because Jupyterlab is a browser-based IDE, we can type the command below to inhibit the activation in browser on server side.

```
(ENV)$ jupyter-lab --no-browser --port=9000
```

After that, it should give messages ending with

```
[I 22:19:00.654 LabApp] Serving notebooks from local directory: /home/username/anaconda3/envs
[I 22:19:00.654 LabApp] Jupyter Notebook 6.1.1 is running at:
[I 22:19:00.654 LabApp] http://localhost:9000/
[I 22:19:00.654 LabApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).

```

### A bridge for connecting to remote server

Because we are using port=9000 in remote server for running Jupyterlab, we have to create a local port as a bridge to catch the corresponding data. In practice, we can realize it by

```
ssh -N -f -L localhost:8888:localhost:9000 -p 22 daweilin@greatlakes.arc-ts.umich.edu
```

Finally, we should be able to open Jupyterlab UI in our browser with an URL: `localhost:8888` after verification.

### One-line command to running Jupyterlab on server (UPDATE)

The previous way requires two terminals which sometimes somehow causes issues (listed below). A more convenient and stable way is to apply the command below
```
sudo ssh -L 8888:127.0.0.1:9000 -p 22 username@greatlakes.arc-ts.umich.edu
```
You may want to replace the ip-address with your own. Besides, if you would like to see real-time logs, you may want to apply `-v` after `ssh` command.



---
## Issues
#### Connetion refused

After initializing Jupyterlab without browser on server side, I applied `ssh` to make a tunnel with port 8888 but it failed and released an error message:
```
channel 2: open failed: connect failed: Connection refused
```

To solve the problem, I firstly use 
```
sudo lsof -i -P -n | grep LISTEN
```
in order to check all the occupied ports. Before you restart/initialize a new ssh process, you may want to kill processes and shut down tunnels.
```
fuser -n tcp -k [PORT Number]
```
Finally, I made a new connection to server by ssh, but I didn't type the URL in my browser for **few minutes**. By doing so, I expected the connection required more time for setting up. The way works for me. 

## Reference

1.  [OpenSSH installation in Ubuntu.](https://linuxize.com/post/how-to-enable-ssh-on-ubuntu-18-04/)
2.  [Running a notebook server](https://jupyter-notebook.readthedocs.io/en/stable/public_server.html)
3.  [Config file and command line options](https://jupyter-notebook.readthedocs.io/en/stable/config.html)
4.  [Use Jupyter notebook remotely](https://amber-md.github.io/pytraj/latest/tutorials/remote_jupyter_notebook)
5.  [Working with Jupyter notebook on a remote server](https://www.blopig.com/blog/2018/03/running-jupyter-notebook-on-a-remote-server-via-ssh/)
