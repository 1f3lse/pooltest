# vulners-scanner
# Description
PoC of a host-based vulnerability scanner, which uses vulners.com API. Detects operating system, collects installed packages and checks vulnerabilities in it.
# Supported OS
Currently support collecting packages for these operating systems:
* Debian-based (debian, kali, ubuntu)
* Rhel-based (redhat, centos, fedora)

# Python version
Lazy and Advanced versions were tested on a python2.6, python2.7, python3.5. If you found any bugs, don't hesitate to open issue

# Docker support
Experimental support of detecting vulnerabilities in running docker containers (only advanced script). Need to activate it changing `checkDocker=False` to `checkDocker=True` in linuxScanner.py

# How to use

* Lazy scanner
The simplest script to show vulners.com API capabilities. Just run script and it will return all found vulnerabilities:
```
# git clone https://github.com/videns/vulners-scanner
# cd vulners-scanner
# ./lazyScanner.py
OS Name - debian, OS Version - 8
Total provided packages: 315
{
    "data": {
        "vulnerabilities": [
            "DSA-3644",
            "DSA-3626"
        ],
        "packages": {            
            "openssh-client 1:6.7p1-5+deb8u2 amd64": {
                "DSA-3626": [
                    {
                        "bulletinVersion": "1:6.7p1-5+deb8u3",
                        "providedVersion": "1:6.7p1-5+deb8u2",
                        "bulletinPackage": "openssh-client_1:6.7p1-5+deb8u3_all.deb",
                        "result": true,
                        "operator": "lt",
                        "OSVersion": "8",
                        "providedPackage": "openssh-client 1:6.7p1-5+deb8u2 amd64"
                    }
                ]
            }
            "fontconfig-config 2.11.0-6.3 all": {
                "DSA-3644": [
                    {
                        "bulletinVersion": "2.11.0-6.3+deb8u1",
                        "providedVersion": "2.11.0-6.3",
                        "bulletinPackage": "fontconfig-config_2.11.0-6.3+deb8u1_all.deb",
                        "result": true,
                        "operator": "lt",
                        "OSVersion": "8",
                        "providedPackage": "fontconfig-config 2.11.0-6.3 all"
                    }
                ]
            },
            "libfontconfig1 2.11.0-6.3 amd64": {
                "DSA-3644": [
                    {
                        "bulletinVersion": "2.11.0-6.3+deb8u1",
                        "providedVersion": "2.11.0-6.3",
                        "bulletinPackage": "libfontconfig1_2.11.0-6.3+deb8u1_all.deb",
                        "result": true,
                        "operator": "lt",
                        "OSVersion": "8",
                        "providedPackage": "libfontconfig1 2.11.0-6.3 amd64"
                    }
                ]
            }
        }
    },
    "result": "OK"
}
Vulnerabilities:
DSA-3644
DSA-3626
```

* Advanced scanner.
Detect OS in a several ways. Supports running docker containers scan (need to activate manually in a file)
```
# git clone https://github.com/videns/vulners-scanner
# cd vulners-scanner
# ./linuxScanner.py

             _
__   ___   _| |_ __   ___ _ __ ___
\ \ / / | | | | '_ \ / _ \ '__/ __|
 \ V /| |_| | | | | |  __/ |  \__ \
  \_/  \__,_|_|_| |_|\___|_|  |___/

==========================================
Host info - Host machine
OS Name - Darwin, OS Version - 15.6.0
Total found packages: 0
==========================================
Host info - docker container "java:8-jre"
OS Name - debian, OS Version - 8
Total found packages: 166
Vulnerable packages:
    libgcrypt20 1.6.3-2+deb8u1 amd64
        DSA-3650 - 'libgcrypt20 -- security update', cvss.score - 0.0
    libexpat1 2.1.0-6+deb8u2 amd64
        DSA-3597 - 'expat -- security update', cvss.score - 7.8
    perl-base 5.20.2-3+deb8u4 amd64
        DSA-3628 - 'perl -- security update', cvss.score - 0.0
    gnupg 1.4.18-7+deb8u1 amd64
        DSA-3649 - 'gnupg -- security update', cvss.score - 0.0
    gpgv 1.4.18-7+deb8u1 amd64
        DSA-3649 - 'gnupg -- security update', cvss.score - 0.0
```

