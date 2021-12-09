# ssl

Install mkcert
----------------
https://github.com/FiloSottile/mkcert

Install mkcert on Ubuntu / Debian
To install mkcert on any Ubuntu or Debian system, first, install certutil dependencies:
```
sudo apt-get update
sudo apt install wget libnss3-tools
```
Once this has been installed, download mkcert binary package from Github. Check mkcert releases page for the latest version.
```
curl -s https://api.github.com/repos/FiloSottile/mkcert/releases/latest| grep browser_download_url  | grep linux-amd64 | cut -d '"' -f 4 | wget -qi -
```
Once the file has been downloaded, make the file executable and place the binary under /usr/loa/bin
```
mv mkcert-v*-linux-amd64 mkcert
chmod a+x mkcert
sudo mv mkcert /usr/local/bin/
```

Now create certificate
```
mkcert -install
mkcert example.com localhost 127.0.0.1 ::1
```
```
mkcert -CAROOT
export CAROOT=your rootCA.pem file location
```
