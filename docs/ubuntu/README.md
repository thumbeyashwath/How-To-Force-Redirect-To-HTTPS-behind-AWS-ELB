
# Security
If you wish to install only security updates the following will work. First it lists all upgradeable packages, 
filter out only the ones coming from a security repo, cut the returned strings at the first field, 
and then passes them to apt-get install for package update.
```shell
sudo apt list --upgradable | grep security |cut -d\/ -f1
sudo apt list --upgradable | grep security |cut -d\/ -f1|xargs sudo apt-get install -y
```


## Unattended installation
```shell
sudo apt install unattended-upgrades
systemctl status unattended-upgrades
```


# cat /etc/apt/apt.conf.d/50unattended-upgrades
```shell
Unattended-Upgrade::Allowed-Origins {
        "${distro_id}:${distro_codename}";
        "${distro_id}:${distro_codename}-security";
        // Extended Security Maintenance; doesn't necessarily exist for
        // every release and this system may not have it installed, but if
        // available, the policy for updates is such that unattended-upgrades
        // should also install from here by default.
        "${distro_id}ESM:${distro_codename}";
//      "${distro_id}:${distro_codename}-updates";
//      "${distro_id}:${distro_codename}-proposed";
//      "${distro_id}:${distro_codename}-backports";
};
Unattended-Upgrade::Package-Blacklist {
      "linux-headers*";
      "linux-image*";
      "linux-generic*";
      "linux-modules*";
};
```


```shell
sudo unattended-upgrades --dry-run --debug
```
Enable at 

```shell
/etc/apt/apt.conf.d/20auto-upgrades
/etc/apt/apt.conf.d/10periodic
```
# cat /etc/apt/apt.conf.d/10periodic
```shell
APT::Periodic::Update-Package-Lists "1";
APT::Periodic::Download-Upgradeable-Packages "1";
APT::Periodic::AutocleanInterval "7";
APT::Periodic::Unattended-Upgrade "1";
```
Reference:
https://phoenixnap.com/kb/automatic-security-updates-ubuntu
