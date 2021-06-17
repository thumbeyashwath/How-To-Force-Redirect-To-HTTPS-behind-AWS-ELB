
# Security
If you wish to install only security updates the following will work. First it lists all upgradeable packages, 
filter out only the ones coming from a security repo, cut the returned strings at the first field, 
and then passes them to apt-get install for package update.
```shell
sudo apt list --upgradable | grep security |cut -d\/ -f1|xargs sudo apt-get install -y
```
