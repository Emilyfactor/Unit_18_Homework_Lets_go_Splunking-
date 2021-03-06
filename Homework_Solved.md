## Unit 18 Homework: Lets go Splunking!

### Scenario

You have just been hired as an SOC Analyst by Vandalay Industries, an importing and exporting company.
 
- Vandalay Industries uses Splunk for their security monitoring and have been experiencing a variety of security issues against their online systems over the past few months. 
 
- You are tasked with developing searches, custom reports and alerts to monitor Vandalay's security environment in order to protect them from future attacks.


### System Requirements 

You will be using the Splunk app located in the Ubuntu VM.


### Your Objective 

Utilize your Splunk skills to design a powerful monitoring solution to protect Vandaly from security attacks.

After you complete the assignment you are asked to provide the following:

- Screen shots where indicated.
- Custom report results where indicated.

### Topics Covered in This Assignment

- Researching and adding new apps
- Installing new apps
- Uploading files
- Splunk searching
- Using fields
- Custom reports
- Custom alerts

Let's get started!

---

## Vandalay Industries Monitoring Activity Instructions


### Step 1: The Need for Speed 

**Background**: As the worldwide leader of importing and exporting, Vandalay Industries has been the target of many adversaries attempting to disrupt their online business. Recently, Vandaly has been experiencing DDOS attacks against their web servers.

Not only were web servers taken offline by a DDOS attack, but upload and download speed were also significantly impacted after the outage. Your networking team provided results of a network speed run around the time of the latest DDOS attack.

**Task:** Create a report to determine the impact that the DDOS attack had on download and upload speed. Additionally, create an additional field to calculate the ratio of the upload speed to the download speed.


1.  Upload the following file of the system speeds around the time of the attack.
    - [Speed Test File](resources/server_speedtest.csv)

2. Using the `eval` command, create a field called `ratio` that shows the ratio between the upload and download speeds.
   - Hint: The format for creating a ratio is: `| eval new_field_name = 'fieldA'  / 'fieldB'`
      
3. Create a report using the Splunk's `table` command to display the following fields in a statistics report:
    - `_time`
    - `IP_ADDRESS`
    - `DOWNLOAD_MEGABITS`
    - `UPLOAD_MEGABITS`
    - `ratio`
  
   Hint: Use the following format when for the `table` command: `| table fieldA  fieldB fieldC`

Solution syntax: 

source="server_speedtest.csv" | eval ratio= UPLOAD_MEGABITS/DOWNLOAD_MEGABITS | table_time IP_ADDRESS DOWNLOAD_MEGABITS UPLOAD_MEGABITS ratio


![image](https://user-images.githubusercontent.com/96030770/166628323-bc975b86-7279-4c27-b89d-5e251104dd32.png)


4. Answer the following questions:

    - Based on the report created, what is the approximate date and time of the attack?
            
            02/23/2020 14:30:00
            
![image](https://user-images.githubusercontent.com/96030770/166630113-65f98820-913c-4a99-862b-f265c187ac6a.png)

 
   - How long did it take your systems to recover?
           
           Approximately 8 hours: between the hours of 14:30:00 to 22:30:00

![image](https://user-images.githubusercontent.com/96030770/166629123-a6bc7c4b-baea-4019-8e0a-a71ff4a6c0fb.png)


Submit a screen shot of your report and the answer to the questions above.
 
### Step 2: Are We Vulnerable? 

**Background:**  Due to the frequency of attacks, your manager needs to be sure that sensitive customer data on their servers is not vulnerable. Since Vandalay uses Nessus vulnerability scanners, you have pulled the last 24 hours of scans to see if there are any critical vulnerabilities.

  - For more information on Nessus, read the following link: https://www.tenable.com/products/nessus

**Task:** Create a report determining how many critical vulnerabilities exist on the customer data server. Then, build an alert to notify your team if a critical vulnerability reappears on this server.

1. Upload the following file from the Nessus vulnerability scan.
   - [Nessus Scan Results](resources/nessus_logs.csv)

2. Create a report that shows the `count` of critical vulnerabilities from the customer database server.
   - The database server IP is `10.11.36.23`.
   - The field that identifies the level of vulnerabilities is `severity`.

       > Solution Syntax:
            - source="nessus_logs.csv" dest_ip"10.11.36.23" severity="*" 

![image](https://user-images.githubusercontent.com/96030770/166635206-083cb914-e7cf-499d-aafb-e4b96d0be9d5.png)

![image](https://user-images.githubusercontent.com/96030770/166636729-1dc0f93a-b098-4b0e-b28c-abf7b51b0041.png)
      
      
3. Build an alert that monitors every day to see if this server has any critical vulnerabilities. If a vulnerability exists, have an alert emailed to `soc@vandalay.com`.

![image](https://user-images.githubusercontent.com/96030770/166636873-bf989e90-fd49-4fab-8283-4185c0e5397b.png)

![image](https://user-images.githubusercontent.com/96030770/166636972-53309e10-f0b3-4f41-b344-fbb852f4c06f.png)

![image](https://user-images.githubusercontent.com/96030770/166636799-f56e5ed6-6512-4e4f-9394-3ad25635b998.png)


Submit a screenshot of your report and a screenshot of proof that the alert has been created.


### Step 3: Drawing the (base)line

**Background:**  A Vandaly server is also experiencing brute force attacks into their administrator account. Management would like you to set up monitoring to notify the SOC team if a brute force attack occurs again.


**Task:** Analyze administrator logs that document a brute force attack. Then, create a baseline of the ordinary amount of administrator bad logins and determine a threshold to indicate if a brute force attack is occurring.

1. Upload the administrator login logs.
   - [Admin Logins](resources/Administrator_logs.csv)

2. When did the brute force attack occur?
   - Hints:
     - Look for the `name` field to find failed logins.
     - Note the attack lasted several hours.

![image](https://user-images.githubusercontent.com/96030770/166841311-baf505e3-d3fb-4925-9e6d-97eff490dac2.png)


3. Determine a baseline of normal activity and a threshold that would alert if a brute force attack is occurring.

   > Attacks starts Feb 21, 2020 between 8 am and 2 pm

I would suggest normal activity would be 25 login attempts per hour before the Brute Force alert is triggerd.

4. Design an alert to check the threshold every hour and email the SOC team at SOC@vandalay.com if triggered. 


![image](https://user-images.githubusercontent.com/96030770/166842374-d1ecf038-4929-4d0b-82ae-a4abb48ae282.png)

![image](https://user-images.githubusercontent.com/96030770/166842425-53bbe034-4e81-4825-b43f-7ab70a6a21d0.png)

![image](https://user-images.githubusercontent.com/96030770/166842473-acdc5bec-1518-4d7d-bef8-08a06088f167.png)


Submit the answers to the questions about the brute force timing, baseline and threshold. Additionally, provide a screenshot as proof that the alert has been created.
 
 
### Your Submission
  
In a word document, provide the following:
  - Answers to all questions where indicated. 
  - Screenshots where indicated.

---

?? 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.

