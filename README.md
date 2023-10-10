# URL Shortener Blitz Documentation

## Table of Contents
1. [Introduction](#introduction)
2. [QA Activities](#qa-activities)
3. [Issue Remediation](#issue-remediation)
4. [Test Results](#test-results)
5. [Monitoring and Log Information](#monitoring-and-log-information)

---

## 1. Introduction

The URL Shortener is a popular application that has recently seen increased demand. To ensure its reliability and performance, we conducted a blitz test to simulate the load of 14,000 users accessing the application simultaneously. This documentation outlines the activities of the Quality Assurance (QA) team, the steps taken to remediate any issues that arose, and the test results before and after the blitz.

### 1.1. Initial Configurations

<img width="931" alt="Screenshot 2023-10-09 at 7 46 35 PM" src="https://github.com/NMonKLabs77/Blitz2/assets/139259756/7c2f08eb-0498-4c36-abc6-5ff22b69c0f6">

- Application.py
  
<p>I imported the logging Python module, which effectively logs messages about my application.</p> 
<p>logging.basicConfig() is used to set the basic configuration for the login module.</p>

- NGINX

<img width="395" alt="Screenshot 2023-10-09 at 9 44 50 PM" src="https://github.com/NMonKLabs77/Blitz2/assets/139259756/83de8c47-d72f-455f-809b-01dd174684f5">


<img width="1440" alt="Screenshot 2023-10-09 at 9 45 04 PM" src="https://github.com/NMonKLabs77/Blitz2/assets/139259756/f9c48ce1-c034-4e2a-9f0a-b4bccd9e914a">
  

<p>CD into NGINX's .conf file</p>
<p>I changed the value of worker_processes from "Auto" to "8".</p>
<p>Uncomment all the lines with gzip</p>

## 2. QA Activities<a name="qa-activities"></a>

### Summary of QA Activities

- The QA engineer conducted a blitz test by sending 14,000 requests to the server to simulate heavy user traffic.
- The goal was to assess the application's performance and scalability and thus any issues that may arise.
- The QA engineer monitored the error rates.

## 3. Issue Remediation

<p><em>What was the issue?</em></p>

The issue was that the URL Shortener was not able to handle an influx of 14,000 requests at once. 1,072 users got an error.

### Steps Taken to Remediate the Issue

1. **Performance Analysis**: After the blitz test, I analyzed the performance metrics and identified that the application struggled to handle the high load possibly due to the ec2.
   It was most likely due to the ec2 being a t2.medium instance which is in the general purpose family with only 2 vCPUs, and 4.0 GiB of memory. This is not powerful enough to handle such an amount of
   load at once. At this point, it was clear that I first needed to upgrade to a larger more robust instance.


6. **Scaling Resources**: We scaled up the server resources, including CPU and memory by using a t2.2xlarge EC2 Instance which has 8vCPUs, and 32 GiB of memory.


8. **Testing and Retesting**: After implementing these changes, we thoroughly tested the application again to ensure that the issues were resolved.

## 4. Test Results

### Test Results

<img width="891" alt="Screenshot 2023-10-09 at 10 23 17 PM" src="https://github.com/NMonKLabs77/Blitz2/assets/139259756/b7279d19-e004-4a5b-97e8-19d7291cedc6">

- Error Rate: 1072
- Server Resource Utilization: 100%

Test- Results after redeploying:

I redeployed the application which is not running on a t2.2xlarge instance and gave it a stress test. It was not affected one bit.

## 5. Monitoring and Log Information

During the blitz test and subsequent remediation process, we monitored various aspects of the application. 


---

By following these steps and closely monitoring the application's performance, we successfully addressed the challenges posed by the blitz test and improved the URL Shortener's reliability and responsiveness for its users. 
