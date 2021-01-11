# Milestone3
In the third milestone, we compile relational algebra queries into a physical query plan of
MapReduce jobs.<br> The MapReduce jobs can then be executed directly on Hadoop by the intermediate of 
Python luigi module: which is a workflow engine that can execute MapReduce jobs Locally or
on hadoop (among many other things).
We will use the following commands line to evaluate/execute a task
#### Locally
python3.6 ra2mr.py SelectTask --querystring "\select_{gender='female'} Person;" --exec-environment LOCAL --local-scheduler <br>
#### On hadoop
PYTHONPATH=. luigi --module ra2mr SelectTask --querystring "\select_{gender='female'} Person;"<br> --exec-environment HDFS --local-scheduler<br>
To execute tests locally, we will use the pytest module by running the command: pytest test_e2e.py or
pytest ra2mr.py. <br>
The unit tests set the task parameter exec_environment to MOCK. All files are then
kept in main memory only. This is intended for unit testing.
### Fixing VirtualBox problem for linux users<br>
The problem is that the module is not signed and therefore not loaded with the kernel.<br>
This will happen if your computer has the SecureBoot mode activated, something very common in modern equipment.
That's why you'll get this error opening any machine in the virtual box (Kernel driver not installed (rc=-1908))<br>
Do the following steps to sign a driver, and it is loaded as a kernel module, on Ubuntu systems and also on Debian 9:
#### Install the mkutil package to be able to do signed:
sudo apt-get update<br>
sudo apt-get upgrade<br>
sudo apt-get install mokutil<br>
#### Generate the signature file:
openssl req -new -x509 -newkey rsa:2048 -keyout MOK.priv -outform DER -out MOK.der -nodes -days 36500 -subj "/CN=VirtualBox/"
#### Add it to the kernel:
sudo /usr/src/linux-headers-$(uname -r)/scripts/sign-file sha256 ./MOK.priv ./MOK.der $(modinfo -n vboxdrv)
#### Register it for the Secure Boot. 
IMPORTANT! That will ask you for a password, put the one you want, you will only have to use it once in the next reboot.<br>
sudo mokutil --import MOK.der
#### Finally, restart the computer.
Enroll MOK -> Continue ->, and it will ask you for the password, and it's done.
### Steps for setting up the Claudera VM:
1- Download the Cloudera VM: <a href="https://www.cloudera.com/downloads/quickstart_vms/5-13/config.html"> Link >></a><br> 
2- Change the keyboard layout by running the command: setxkbmap fr <br>
To do this automatically every time, extend your .bashrc with the command: echo "setxkbmap us" >> ~/.bashrc<br>
3- Mount a shared folder so that we can easily share data between the host, and the virtual machine: 
<a href="https://www.youtube.com/watch?v=_VF8vbUQWX0"> Link >> </a><br>
4- Open a terminal. we’ll need a more modern Python version and some extra modules.
#### Download Python 3.6:
wget https://www.python.org/ftp/python/3.6.5/Python-3.6.5.tar.xz<br>
xz -d Python-3.6.5.tar.xz<br>
tar -xvf Python-3.6.5.tar<br>
cd Python-3.6.5<br>
./configure --prefix=/usr/local
4- Let's build (compile) the source, this can take a while<br>
make<br>
sudo make altinstall<br>
cd ..<br>
sudo rm -rf Python*<br>
#### Install PIP:
wget https://bootstrap.pypa.io/get-pip.py<br>
sudo /usr/local/bin/python3.6 get-pip.py<br>
rm -f get-pip.py<br>
#### Install further modules that we will need:
sudo /usr/local/bin/python3.6 -m pip install luigi<br>
sudo /usr/local/bin/python3.6 -m pip install sqlparse<br>
sudo /usr/local/bin/python3.6 -m pip install radb<br>
sudo /usr/local/bin/python3.6 -m pip install pytest<br>
sudo /usr/local/bin/python3.6 -m pip install pytest-repeat<br>
sudo /usr/local/bin/python3.6 -m pip uninstall -y antlr4-python3-runtime<br>
sudo /usr/local/bin/python3.6 -m pip install antlr4-python3-runtime==4.7<br>
### Useful links: <br>
<p>Python yield usage and concept:
<a href="https://dzone.com/articles/when-to-use-yield-instead-of-return-in-python"> Link >> </a></p>
<p>To understand well the concept of mapreduce we can have a look at the chapter on “Workflow Systems” for MapReduce engines in chapter 2.4.1 of the
book “Mining Massive Datasets”</p>