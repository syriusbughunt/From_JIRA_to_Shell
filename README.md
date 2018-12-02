# Reverse shell from JIRA
Since I haven't found any well explained articles on how to get reverse shell from JIRA web application server, I thought it could be a good idea to cover this subject with the pentesters community.  
  
## 0x00 : Introduction on JIRA&nbsp; <img src="https://raw.githubusercontent.com/syriusbughunt/From_JIRA_to_Shell/master/img/JIRA.jpg" width="20"/>
  
JIRA Software is a powerful platform that combines issue collection and agile project management capabilities into a single application. Using JIRA helps you plan and organize tasks, workflows, and reports for your agile team more efficiently.  
  
I've seen many environment in my career where the JIRA web application is installed without or with poor credentials which maybe some admins ignore the fact that we can get remote code execution on this web app. 
  
## 0x01 : Locate the JIRA servers on the LAN&nbsp; <img src="https://raw.githubusercontent.com/syriusbughunt/From_JIRA_to_Shell/master/img/0x01.png" width="35"/>
  
Usually, JIRA servers are configured by default to run on port 8080 but I've seen many times where the bind port was changed to 80 (HTTP) or 443 (HTTPS). For discovering what is on the LAN, I would choose masscan available on the link below:  
  
→ https://github.com/robertdavidgraham/masscan  
  
Let's say that you are inside a local area network with the subnet *192.168.255.0* and your local IP address is *192.168.123.45* and wish to perform a complete network scan to discover those JIRA servers. The syntax for running masscan in that I would use would be:  
```
./masscan 192.168.0.0-192.168.255.255 -p80,443,8080 -oL JIRA.where-are-you.txt --max-rate 10000 --open --banners -sS -Pn -n --randomize-hosts -v --send-eth
  
