# Rifky Taufikurrohman
Question-One :

-Basic Linux

a) Please provide a cronjob to Housekeeping log in /var/log/nginx/ if log more than 14 days
```
* * * * *  find  /path/to/*.log -mtime +14 -exec rm -f {} \;
```
b) Please provide a logrotate script in /etc/logrotate.d/ to compress log in /var/log/nginx/ if more than 100MB

```
# cat -n /etc/logrotate.d/nginx
/var/log/nginx/*log {
        daily
        missingok
        rotate 10
        compress
        delaycompress
        notifempty
        create 0644 nginx
        sharedscripts
        postrotate
                /bin/kill -USR1 `cat/run/nginx.pid 2>/dev/null 2>/dev/null || true
        endscript
}
```
Question-two :

-Linux Administration

Please provide file of /etc/nginx/nginx.conf to do the the job
```
upstream backend {
   # no load balancing method is specified for Round Robin
   server appservern1;
   server appservern2;
}
```

Question-Three :

-Office 365
Assuming you are O365 Administrator in our company, suddenly we have spam attack to our organization with this details below:
```
- From : itadmin@xyz.com ; (207.18.13.24)
- Subject : YOUR PASSWORD HAS BEN EXPIRED
- to : all member
```

a. Tell us step-by-step to prevent that spam attack appear again in our mailbox
```
1. Pull emails indicated as spam with Content Search, Microsoft 365 Admin Center > Security & Compliance > Search > Content Search
2. Click + New Search > Enter Query according to email information indicated sending spam: itadmin@xyz.com
3. In specific locations select Modify > select all Exchange Email > Save
4. After that Save & Run and fill in the name of the content search. If it is finished, it can be analyzed the message header
5. Download Original Item > Open the Message File
6. After the message file is opened select File > Properties > Select All Internet Headers > Copy
7. Go to the https://mha.azurewebsites.net/ website to analyze the internet header. Paste the copied internet header and then analyze the header
8. Header information will appear, Analyze the header
9. Then Analyze IP Sender (207.18.13.24) via https://whatismyipaddress.com/ and why spam can enter via x-forefront-antispam-report
10. If the IP is not in cooperation with our company, please block it with the sender. Exchange Admin Center > Protection > Connection Filter ( To Block IP) & Spam Filter (to block email addresses & domains) > Edit
11. After IP and email address/domain of the spammer are blocked, delete spam message via Powershell.
```
b. Please provide powershell script to recall the spam mail from every mailbox
```
  $UserCredential = Get-Credential
  $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://ps.compliance.protection.outlook.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection
  Import-PSSession $Session
```
Command line above to be connected to security & compliance. After connect delete spam by name content search.

Run the following command line :
```
  New-ComplianceSearchAction -SearchName "Name Content Search" -Purge -PurgeType HardDelete  (Select HardDelete/SoftDelete)
```
To see the results run this command line :
```
Get-ComplianceSearchAction -Identity "Name Content Search_Purge" | Format-List
```

## Thankyou
