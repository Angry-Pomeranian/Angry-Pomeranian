## Unit 18 Homework: Lets go Splunking!

Nicole Kemp

21st of April 2022

Hw wk18


---

# Step 1: The Need for Speed 

Note that My host and sourcetype name will be diffrent compared to your machine.  




## Task 1 Upload:
![image](https://user-images.githubusercontent.com/91113466/164487623-aac071df-4d71-4ccf-8856-bd548352b32a.png)

## Task 2 EVAL Command: 

       Answer: 'source="server_speedtest.csv" host="2f9003817211" sourcetype="Hw(server speed test)" | eval ratio='DOWNLOAD_MEGABITS'/'UPLOAD_MEGABITS'

Insert screenshot:

## Task 3 Speed Test Reort (table report):

       Answer: `source="server_speedtest.csv" host="2f9003817211" sourcetype="Hw(server speed test)" | eval ratio='DOWNLOAD_MEGABITS'/'UPLOAD_MEGABITS' | sort _time | table _time IP_ADDRESS UPLOAD_MEGABITS DOWNLOAD_MEGABITS ratio`

insert screenshot:


## Report:

## Task 4 Area chart/line chart:

        Answer: I anyalised the attacks by changing the display to a line chart. However i also took a screenshot of it as an area chart since line charts can be hard to read.

Insert screenshot:


## Answer the following questions:

Q1: Based on the report created, what is the approximate date and time of the attack?
      
      Answer: The attack took place on `02/23/2020 at 14:30`, and it lasted till `02/23/2020 at 23:30`. It has the biggest impact on the 22nd (lowest part in the chart), the download speed dropped dramatically down from `105.91Mbps to 7.87 Mbps`. After the attack, the speed returned to normal `(over 122.91 Mbps)`.

Q2: How long did it take your systems to recover?

      Answer: 9 hours! oof.

___
# Step 2: Are We Vulnerable? 

## Task 1 Upload:
Screenshot


## Task 2 The query command: 

         Answer: `source="nessus_logs.csv" host="2f9003817211" sourcetype="nessus_logs.csv" dest_ip="10.11.36.23" | eval CRITICAL=IF(severity="critical", "Critical", "Non-Critical") | stats count by CRITICAL`


## Task 3 Make an Alert:
screenshot

## Task 4 Report:
      There are 49 critical database server vulnerabilities, and 194 Non-Critical. (see task 2)
___
# Step 3: Drawing the (base)line

## Task 1 Upload:
screenshot
## Task 2 The query command: 

         source="Administrator_logs.csv" host="2f9003817211" | stats count by name | sort -count | eval Bruteforce=if(name="An account failed to log on" AND count>5, "Potential Brute Force", "Not Brute Force")

## Task 3 Make an Alert:
screenshot

## Task 4 Report:

         By examining the 'name' field for "An account failed to log on" I was able to determine the time of the attack, the baseline and the threshold...

         The brute force attack occurred from 9:00 a.m. until 2:00 p.m. on 2/21/2020 for a total of 5 hours.

         Based on the logs, the the baseline is 5 to 35 logs an hour. The threshold will be set at 40 or more login attempts in an hour and the alert will be sent to SOC@vandalay.com when triggered.


# Congrats you reached the end! "Dobby is a free elf! "
  
