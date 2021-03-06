Lab : calculate customer total
project dir : mr-billing
you can also open the project in eclipse

== STEP 1)
    $  cd mr-billing
    edit the file : src/hi/mr/BillingTotal.java


== STEP 2) complete the TODO items
Answer : src/hi/mr/BillingTotalAnswer.java


== STEP 3) compile the code:
  $ cd mr-billing
  $ ../compile2.sh

this should create a jar file called 'a.jar'


== STEP 4)
Now it is time to copy the sample input into HDFS
for hadoop 1
    $ hadoop dfs -mkdir  <your name>/billing/in
    $ hadoop dfs -put  ../../data/billing-data/sample.txt   <your name>/billing/in/

for hadoop 2
    $ hdfs dfs -mkdir  <your name>/billing/in
    $ hdfs dfs -put  ../../data/billing-data/sample.txt   <your name>/billing/in/

== STEP 5)
we will run this jar file
  $ hadoop jar a.jar  hi.mr.BillingTotal   <your name>/billing/in/sample.txt   <your name>/billing/out


== STEP 6)
Once the mr job is done, inspect the output file:
for hadoop 1
  $ hadoop  dfs -cat <your name>/billing/out/part-r-00000

for hadoop 2
  $ hdfs  dfs -cat <your name>/billing/out/part-r-00000
or
Browse HDFS file system.  Navigate to '/user/<your user name>/billing/out' dir
(see ../getting-started.txt for detailed instructions)


== STEP 7)
Once the sample data is working, lets try this on more data.

Generate more (random) sample data
    $  python ../../data/billing-data/gen-billing-data.py
This would generate a bunch of *.log files

Inspect a log file
    $  head  billing-2012-01-01.log

Quiz : How many records have we generated?

Now lets copy the newly generated log files into HDFS
    $  hdfs  dfs -put   *.log    <your name>/billing/in/

Verify the files are there
    $  hdfs  dfs -ls <your name>/billing/in


== STEP 8)
run mr again on this new data
  $ hadoop jar a.jar  hi.mr.BillingTotal   <your name>/billing/in   <your name>/billing/out2
note 1 : we are supplying an input dir (not a single file)
note 2 : specified a different output dir


== STEP 9)
inspect the output from JobTracker UI
(see ../getting-started.txt, STEP 4, for detailed instructions)


== STEP 10)
examine the job stats from job tracker UI
go to  http://<job tracker>:50030
       http://localhost:50030

Find the job under 'completed jobs' section
Click on it
inspect the stats
