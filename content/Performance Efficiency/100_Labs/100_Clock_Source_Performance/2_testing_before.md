---
title: "Testing Performance of both nodes before clock changes"
menutitle: "Test performance"
date: 2020-06-09T12:00:00-04:00
chapter: false
weight: 2
pre: "<b>2. </b>"
---

Now that we have two EC2 machines, one Xen based EC2 and one Nitro/KVM based EC2, we can run a simple test to see the speed in which is can return time of day. This test program was installed on each machine under /tmp/time_test.py. The program will simply request the time of day from a local c-library one million times.

## The time_test.py code
```
#!/usr/bin/python3
import time

_gettimeofday = None
def gettimeofday():
  import ctypes
  global _gettimeofday

  if not _gettimeofday:
    _gettimeofday = ctypes.cdll.LoadLibrary("libc.so.6").gettimeofday

  class timeval(ctypes.Structure):
    _fields_ = \
    [
      ("tv_sec", ctypes.c_long),
      ("tv_usec", ctypes.c_long)
    ]

  tv = timeval()

  _gettimeofday(ctypes.byref(tv), None)

  return float(tv.tv_sec) + (float(tv.tv_usec) / 1000000)


start_time = time.time()

for x in range(0,1000000):
    gettimeofday()

print("--- %s seconds ---" % (time.time() - start_time))

print("Done")
```
If you wish to bypass using the pre-defined AWS System Manager documents below, you can also run this script interactively on each EC2 node using [AWS Systems Manager Session Manager](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager.html).  


1.	Open the AWS Console (https://console.aws.amazon.com)
1.	In the “Find Services” search bar, type “Systems Manager” and press enter
![BeforeTest1](/Performance/100_Clock_Source_Performance/Images/BeforeTest1.png)
1.	Under “Instances & Nodes” click on “Run Command” and on the left side of the screen again click on “Run a command”
![BeforeTest2](/Performance/100_Clock_Source_Performance/Images/BeforeTest2.png)
1.	In the search bar under Command Document, select “Owner” from the pulldown and then select “Owned by me”.
![BeforeTest3](/Performance/100_Clock_Source_Performance/Images/BeforeTest3.png)
![BeforeTest4](/Performance/100_Clock_Source_Performance/Images/BeforeTest4.png)
1.	You should see 2 SSM documents that have been created for you by the Cloudformation Template.  Click on the one with “runTestScriptdocument” in the name.
![BeforeTest5](/Performance/100_Clock_Source_Performance/Images/BeforeTest5.png)
1.	Scroll down and under “Targets”, select the checkbox next to the two instances that were created from the template.  The should be labeled “XenTimeInstanceTest” and “KVMTimeInstanceTest”
![BeforeTest6](/Performance/100_Clock_Source_Performance/Images/BeforeTest6.png)
1.	Scroll down and uncheck the box that says “Enable writing to an S3 bucket” and then click the “Run” button at the bottom of the screen.
![BeforeTest7](/Performance/100_Clock_Source_Performance/Images/BeforeTest7.png)
1.	You should see the command running on both nodes as “In Progress”. Click the refresh button every few seconds until both boxes show “Success” in their status column.
![BeforeTest8](/Performance/100_Clock_Source_Performance/Images/BeforeTest8.png)
{{% notice info %}}
It will take longer to complete for one node to run than the other. The total time for both to complete should be about 2 minutes if you use the default EC2 instance types.
{{% /notice %}}
1.	You can now click on each Instance ID to see the output of the command that was run. Just click the pulldown for “Step 1 - Output” and you should see the following.  As you noticed, it tells you at the top of the output how long the script took to run in total, as well as the syscalls used during its execution.  In this first example, we can see it ran in 16 seconds and the stat call is the most frequently used.
![BeforeTest9](/Performance/100_Clock_Source_Performance/Images/BeforeTest9.png)
![BeforeTest10](/Performance/100_Clock_Source_Performance/Images/BeforeTest10.png)
1.	In this second instance, we can see that it took 110 seconds and the gettimeofday call used over 99% of the time during its run.
![BeforeTest11](/Performance/100_Clock_Source_Performance/Images/BeforeTest11.png)


{{< prev_next_button link_prev_url="../1_deploy/" link_next_url="../3_change_clock/" />}}
