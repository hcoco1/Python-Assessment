##### Navigation

[Back to Home 🏠](../README.md) | [Back to Technical Assessment ](btechnical_assessment.md)  

## Unit 4 Career Preparation: Challenge

### Problem 1

1.Open the exam.log file.

2.Write a function ip_result that:

- Searches for lines with IP
- Counts the number of each IP
- Puts the results in a dictionary
- Sorts the dictionary
- Puts the results into a file

3.Write a function invalid_user_count that:

- Searches for invalid user logins
- Counts the invalid logins for each user
- Puts the results in a dictionary
- Sorts the dictionary
- Puts the result into a file

4.Write a function failed_logins that:

- Searches for wrong passwords
- Counts the failed logins
- Puts the results in a dictionary
- Sorts the dictionary
- Puts the result in a file

5.Call the functions

```python
import re

def ip_result(filename):
    ip_counts = {}
    with open(filename, 'r') as file:
        for line in file:
            ips = re.findall(r'\b\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}\b', line)
            for ip in ips:
                if ip not in ip_counts:
                    ip_counts[ip] = 1
                else:
                    ip_counts[ip] += 1
    sorted_ip_counts = sorted(ip_counts.items(), key=lambda x: (-x[1], x[0]))
    with open('ips_count.log', 'w') as outfile:
        for ip, count in sorted_ip_counts:
            outfile.write(f"{ip}: {count}\n")
            
def invalid_user_count(filename):
    user_counts = {}
    with open(filename, 'r') as file:
        for line in file:
            if "invalid user" in line:
                user = re.search(r'invalid user (\w+)', line)
                if user:
                    username = user.group(1)
                    if username not in user_counts:
                        user_counts[username] = 1
                    else:
                        user_counts[username] += 1
    sorted_user_counts = sorted(user_counts.items(), key=lambda x: (-x[1], x[0]))
    with open('invalid_users_count.log', 'w') as outfile:
        for user, count in sorted_user_counts:
            outfile.write(f"{user}: {count}\n")

def failed_logins(filename):
    failed_counts = {}
    with open(filename, 'r') as file:
        for line in file:
            if "Failed password" in line:
                failed = re.search(r'for invalid user (\w+)', line)
                if failed:
                    user = failed.group(1)
                else:
                    user = "unknown"
                if user not in failed_counts:
                    failed_counts[user] = 1
                else:
                    failed_counts[user] += 1
    sorted_failed_counts = sorted(failed_counts.items(), key=lambda x: (-x[1], x[0]))
    with open('failed_logins_count.log', 'w') as outfile:
        for user, count in sorted_failed_counts:
            outfile.write(f"{user}: {count}\n")

if __name__ == "__main__":
    filename = "/home/labsuser/exam.log" 
    ip_result(filename)
    invalid_user_count(filename)
    failed_logins(filename)
    
#ips_count.log = {
# 80.237.75.2: 481
# 185.182.56.85: 450
# 212.237.47.236: 358
# 137.74.1.62: 284
# 87.27.92.12: 70
# 192.129.227.186: 26
# 5.255.68.179: 20
# 112.112.102.38: 10
# 178.68.209.126: 10
# 221.148.234.252: 10
# 151.40.221.171: 6
# 123.150.200.121: 5
# 138.19.133.51: 5
# 168.70.37.89: 5
# 197.245.39.234: 5
# 41.59.225.121: 5
# 42.159.246.3: 5
# 80.211.140.131: 4
# 5.8.10.202: 3
# 0.0.0.0: 2
# 5.39.216.134: 2
# 71.6.165.200: 2
# 146.0.75.199: 1
# 163.172.69.249: 1
# 178.15.105.238: 1
# 185.156.177.53: 1
# 185.156.177.8: 1
# 185.222.211.18: 1
# 196.52.43.94: 1
# 213.202.230.144: 1
# 91.121.158.124: 1
# }


```

### Problem 2

Analyze the following code that reads the apache_logs.txt file. Determine what it does. Write your response as code comments.

```python
#Basics imports
import sys
import os

def readfile(f):# This function reads a file. It will be used to reading log files.
    openfile = open(f,"r")

    unique_outfile = open("uniqueIP.txt","w")#Creating file to store logs data
    all_outfile = open("allIP.txt","w")
    ipAndUrl_outfile = open("ipAndUrl.txt","w")

    lines = []
    ipAndUrl = {}
    ip_list = set()
  #reading through each line of the file, and removing the end-of-line.
    for line in openfile:
        lines.append(line.strip('\n'))
    #look at each line I read and find IP addresses and URL.
    for line in lines:
        ip = line.split(" ")[0]
    #adding ip and url to a file
        if ip in ipAndUrl:
            ipAndUrl[ip].append(line.split(" ")[6])
        else:
            ipAndUrl[ip] = [line.split(" ")[6]]
    #writing down every IP address
        all_outfile.write(ip)
        all_outfile.write("\n")

        ip_list.add(ip)
    #adding unique ip to a file
    for ip in ip_list:
        unique_outfile.write(ip)
        unique_outfile.write("\n")
    #writing down which IP addresses asked for which URLs
    for key, value in ipAndUrl.items(): 
        ipAndUrl_outfile.write('%s  %s\n' % (key, value))
    #close all files
    unique_outfile.close()
    ipAndUrl_outfile.close()
    all_outfile.close()
    openfile.close()
# the main function trigger the script.
def Main():
    file=input("please enter a file name: ")

    result = readfile(file)

if __name__ == '__main__':
      Main()
    

    
# #Input = /home/labsuser/apache.txt (file created to test the script)

# apache.txt = {
# 192.168.1.100 - - [01/Mar/2024:10:00:00 +0000] "GET /index.html HTTP/1.1" 200 1234
# 192.168.1.101 - - [01/Mar/2024:10:00:01 +0000] "GET /about.html HTTP/1.1" 404 987
# 192.168.1.102 - - [01/Mar/2024:10:00:02 +0000] "GET /contact.html HTTP/1.1" 200 4321
# 192.168.1.103 - - [01/Mar/2024:10:00:03 +0000] "GET /images/logo.png HTTP/1.1" 304 -
# 192.168.1.104 - - [01/Mar/2024:10:00:04 +0000] "GET /blog HTTP/1.1" 301 345
# 192.168.1.105 - - [01/Mar/2024:10:00:05 +0000] "GET /blog/post1.html HTTP/1.1" 200 6789
# 192.168.1.100 - - [01/Mar/2024:10:00:00 +0000] "GET /index.html HTTP/1.1" 200 1234
# 192.168.1.101 - - [01/Mar/2024:10:00:01 +0000] "GET /about.html HTTP/1.1" 404 987
# 192.168.1.102 - - [01/Mar/2024:10:00:02 +0000] "GET /contact.html HTTP/1.1" 200 4321
# 192.168.1.103 - - [01/Mar/2024:10:00:03 +0000] "GET /images/logo.png HTTP/1.1" 304 -
# 192.168.1.104 - - [01/Mar/2024:10:00:04 +0000] "GET /blog HTTP/1.1" 301 345
# 192.168.1.105 - - [01/Mar/2024:10:00:05 +0000] "GET /blog/post1.html HTTP/1.1" 200 6789
# }

#The script is tool for breaking down logs information like Apache logs. It created three separate files that store the following information: 

# One file to store all ip

# allIP.txt = {
#192.168.1.100
#192.168.1.101
#192.168.1.102
#192.168.1.103
#192.168.1.104
#192.168.1.105
#192.168.1.100
#192.168.1.101
#192.168.1.102
#192.168.1.103
#192.168.1.104
#192.168.1.105
# }

#Another file to store ip and url or routes associated

# ipAndUrl.txt = {
#192.168.1.100  ['/index.html', '/index.html']
#192.168.1.101  ['/about.html', '/about.html']
#192.168.1.102  ['/contact.html', '/contact.html']
#192.168.1.103  ['/images/logo.png', '/images/logo.png']
#192.168.1.104  ['/blog', '/blog']
#192.168.1.105  ['/blog/post1.html', '/blog/post1.html']
# }

#The last file to store uniques ip.

# uniqueIP.txt = {
# 192.168.1.103
# 192.168.1.101
# 192.168.1.105
# 192.168.1.102
# 192.168.1.104
# }

```




##### Navigation

[Back to Home 🏠](../README.md) | [Back to Technical Assessment ](btechnical_assessment.md)  