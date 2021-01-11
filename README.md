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

To execute the tests locally,we will use the pytest module by running the command: pytest test_e2e.py or
pytest ra2mr.py.

### Useful links: <br>
<p>Python yield usage and concept:
<a href="https://dzone.com/articles/when-to-use-yield-instead-of-return-in-python"> Link >> </a>
</p>