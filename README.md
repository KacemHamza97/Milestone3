# Milestone3
In the third milestone, we compile relational algebra queries into a physical query plan of
MapReduce jobs.<br> The MapReduce jobs can then be executed directly on Hadoop by the intermediate of 
Python luigi module: which is a workflow engine that can execute MapReduce jobs Locally or
on hadoop (among many other things).

We will use the following commands line to evaluate/execute a task
### Locally:
python3.6 ra2mr.py SelectTask --querystring "\select_{gender='female'} Person;" --exec-environment LOCAL --local-scheduler <br>
### On hadoop:
PYTHONPATH=. luigi --module ra2mr SelectTask --querystring "\select_{gender='female'} Person;"<br> --exec-environment HDFS --local-scheduler

To execute tests locally, we will use the pytest module by running the command: pytest test_e2e.py or
pytest ra2mr.py. <br>
The unit tests set the task parameter exec_environment to MOCK. All files are then
kept in main memory only. This is intended for unit testing.

### steps for setting up the Claudera VM:
1- change the keyboard layout by running the command: ... <br>
2- mount a shared folder so that we can easily share data: link ....<br>
3- Open a terminal. we’ll need a more modern Python version and some extra modules.<br>
Download Python 3.6
wget https://www.python.org/ftp/python/3.6.5/Python-3.6.5.tar.xz
xz -d Python-3.6.5.tar.xz
tar -xvf Python-3.6.5.tar
cd Python-3.6.5
./configure --prefix=/usr/local
4- Let's build (compile) the source, this can take a while<br>
make
sudo make altinstall
cd ..
sudo rm -rf Python*
Install PIP <br>
wget https://bootstrap.pypa.io/get-pip.py
sudo /usr/local/bin/python3.6 get-pip.py
rm -f get-pip.py
Install further modules that we will need <br>
sudo /usr/local/bin/python3.6 -m pip install luigi
sudo /usr/local/bin/python3.6 -m pip install sqlparse
sudo /usr/local/bin/python3.6 -m pip install radb
sudo /usr/local/bin/python3.6 -m pip install pytest
sudo /usr/local/bin/python3.6 -m pip install pytest-repeat
sudo /usr/local/bin/python3.6 -m pip uninstall -y antlr4-python3-runtime
sudo /usr/local/bin/python3.6 -m pip install antlr4-python3-runtime==4.7



### Useful links: <br>
<p>Python yield usage and concept:
<a href="https://dzone.com/articles/when-to-use-yield-instead-of-return-in-python"> Link >> </a>
</p>
<p>To understand well the concept of mapreduce we can have a look at the chapter on “Workflow Systems” for MapReduce engines in chapter 2.4.1 of the
book “Mining Massive Datasets”</p>