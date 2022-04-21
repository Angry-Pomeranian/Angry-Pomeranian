## Unit 18 Homework: Lets go Splunking!

Nicole Kemp

21st of April 2022

Hw wk18


---

# Step 1: The Need for Speed 

Note that My host and sourcetype name will be diffrent compared to your machine.  

![Task 0 (upload data)](https://user-images.githubusercontent.com/91113466/164487796-e2b73b3d-a7f6-47cb-b65e-06e55c3f0e2b.jpg)



## Task 1 Upload:
![image](https://user-images.githubusercontent.com/91113466/164487623-aac071df-4d71-4ccf-8856-bd548352b32a.png)

## Task 2 EVAL Command: 

       Answer: 'source="server_speedtest.csv" host="2f9003817211" sourcetype="Hw(server speed test)" | eval ratio='DOWNLOAD_MEGABITS'/'UPLOAD_MEGABITS'

![image](https://user-images.githubusercontent.com/91113466/164487875-043f1cb7-0182-4433-86ea-4756e797ab9a.png)

## Task 3 Speed Test Reort (table report):

       Answer: `source="server_speedtest.csv" host="2f9003817211" sourcetype="Hw(server speed test)" | eval ratio='DOWNLOAD_MEGABITS'/'UPLOAD_MEGABITS' | sort _time | table _time IP_ADDRESS UPLOAD_MEGABITS DOWNLOAD_MEGABITS ratio`

![image](https://user-images.githubusercontent.com/91113466/164487936-0eb63219-60b5-47cb-a857-c2d6bb76148c.png)


## Report:

## Task 4 Area chart/line chart:

        Answer: I anyalised the attacks by changing the display to a line chart. However i also took a screenshot of it as an area chart since line charts can be hard to read.

![image](https://user-images.githubusercontent.com/91113466/164487983-9805e5d7-90a1-4d6d-bfd6-31c08d2cfe2d.png)
![image](https://user-images.githubusercontent.com/91113466/164488020-71def407-5de2-4134-8448-07560ab49caa.png)


## Answer the following questions:

Q1: Based on the report created, what is the approximate date and time of the attack?
      
      Answer: The attack took place on `02/23/2020 at 14:30`, and it lasted till `02/23/2020 at 23:30`. It has the biggest impact on the 22nd (lowest part in the chart), the download speed dropped dramatically down from `105.91Mbps to 7.87 Mbps`. After the attack, the speed returned to normal `(over 122.91 Mbps)`.

Q2: How long did it take your systems to recover?

      Answer: 9 hours! oof.

___
# Step 2: Are We Vulnerable? 

## Task 1 Upload:
![image](https://user-images.githubusercontent.com/91113466/164488106-94785249-ad2f-4523-9bc0-320c55f5e5f9.png)


## Task 2 The query command: 

         Answer: `source="nessus_logs.csv" host="2f9003817211" sourcetype="nessus_logs.csv" dest_ip="10.11.36.23" | eval CRITICAL=IF(severity="critical", "Critical", "Non-Critical") | stats count by CRITICAL`
![image](https://user-images.githubusercontent.com/91113466/164488147-f2224d2f-8ee5-4054-b25d-6a8858ee9d4b.png)


## Task 3 Make an Alert:
![image](https://user-images.githubusercontent.com/91113466/164488198-eba1cf5d-370e-467d-b91d-49ae0aeba298.png)
![image](https://user-images.githubusercontent.com/91113466/164488233-e42844a2-5189-40fd-bdb9-36362713980b.png)
![image](https://user-images.githubusercontent.com/91113466/164488271-3dd39e88-23c4-4faa-bbb9-c159eede9663.png)

## Task 4 Report:
      There are 49 critical database server vulnerabilities, and 194 Non-Critical. (see task 2)
___
# Step 3: Drawing the (base)line

## Task 1 Upload:
![image](https://user-images.githubusercontent.com/91113466/164488453-63667f4e-439f-483a-8a93-862785a82fa8.png)
## Task 2 The query command: 

         source="Administrator_logs.csv" host="2f9003817211" | stats count by name | sort -count | eval Bruteforce=if(name="An account failed to log on" AND count>5, "Potential Brute Force", "Not Brute Force")

![image](https://user-images.githubusercontent.com/91113466/164488508-a9ccf0aa-3e41-4cdf-bcbf-14e8dca2221e.png)
![image](https://user-images.githubusercontent.com/91113466/164488551-f5e0484a-0403-468e-8fee-80758fada792.png)


## Task 3 Make an Alert:
![image](https://user-images.githubusercontent.com/91113466/164488661-c14b4982-15cc-4bd1-8081-298e8248c79f.png)
![image](https://user-images.githubusercontent.com/91113466/164488705-25637345-2a1a-4077-affd-d8b28e3423e9.png)
![image](https://user-images.githubusercontent.com/91113466/164488748-45654303-5396-45e3-915b-3b9e3e9c2ada.png)


## Task 4 Report:

         By examining the 'name' field for "An account failed to log on" I was able to determine the time of the attack, the baseline and the threshold...

         The brute force attack occurred from 9:00 a.m. until 2:00 p.m. on 2/21/2020 for a total of 5 hours.

         Based on the logs, the the baseline is 5 to 35 logs an hour. The threshold will be set at 40 or more login attempts in an hour and the alert will be sent to SOC@vandalay.com when triggered.

![image](https://user-images.githubusercontent.com/91113466/164488921-05f6f722-1066-478c-a0ab-b4f881983268.png)


# Congrats you reached the end! "Dobby is a free elf! "
  
