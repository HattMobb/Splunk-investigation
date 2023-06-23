# Splunk-investigation
Investigating suspicious behaviour using Splunk

---


After accessing the logs, quite a few events can be seen: 


![Screenshot 2023-06-22 114630](https://github.com/HattMobb/Splunk-investigation/assets/134090089/7f8869fc-c460-4655-9863-9570690b9cc6)


![image](https://github.com/HattMobb/Splunk-investigation/assets/134090089/7180e443-ac3b-42c1-a734-4402dac90d84)

Creating a new user has the Event ID of 4720. Searching for this ID yields the following results:

![Screenshot 2023-06-22 114835](https://github.com/HattMobb/Splunk-investigation/assets/134090089/f4d86790-41ab-42a0-93e4-bd3ed53e5d66)

![Screenshot 2023-06-22 114905](https://github.com/HattMobb/Splunk-investigation/assets/134090089/c55c7850-5996-4e8b-9e29-303d1a88f42a)

It is evident that there has been a user ` A1berto ` created as a means of trying to impersonate Alberto.

---

![Screenshot 2023-06-22 123839](https://github.com/HattMobb/Splunk-investigation/assets/134090089/a6b29255-b425-4087-b336-02b48c139b13)

Checking logged CLI commands shows only a few results, so it's pretty quick work to locate the command used to add the new user:

` C:\windows\System32\Wbem\WMIC.exe" /node:WORKSTATION6 process call create "net user /add A1berto paw0rd1 `

---

![image](https://github.com/HattMobb/Splunk-investigation/assets/134090089/48943bfe-3da8-4e58-b21e-99fbad2d8190)

The following search checks the main index for all instances of Powershell to narrow down results:

![Screenshot 2023-06-22 125236](https://github.com/HattMobb/Splunk-investigation/assets/134090089/59c50926-9d44-4708-b57c-3cb1c476ef5c)

It can be seen that only 1 user has been using Powershell in the given time period:


![Screenshot 2023-06-22 125309](https://github.com/HattMobb/Splunk-investigation/assets/134090089/83763d8d-c7bf-4f25-8943-d66063a779f3)

---


![image](https://github.com/HattMobb/Splunk-investigation/assets/134090089/233b457b-be44-4bd3-b8bd-ce90557d4c40)

