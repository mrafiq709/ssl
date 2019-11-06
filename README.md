# Create-Valid-SSL-in-localhost-for-XAMPP
SSL

**step 1:** ```Go to-> C:\xampp\apache\crt```

**step 2:** ```create "cert.conf" and "make-cert.bat" file```
**step 3:** ```run "make-cert.bat" file```
**step 4:** ```it will create "site.test" folder and inside it there two file named: "server.crt" and "server.key", then run "server.crt"```
**setp 5:** ```click "install certificate...", then select "local machine", after that seletc "Trusted root certificate authorities".```
**step 6:** ```Go to-> "C:\Windows\System32\drivers\etc\hosts" and add "127.0.0.1 site.test"```


```
Note: If does not work, re-install your apache server or xammp.
```
Refernces:
----------
https://shellcreeper.com/how-to-create-valid-ssl-in-localhost-for-xampp/
