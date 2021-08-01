# MSFTVPN for Linux
- The (unofficial) Microsoft VPN client for Linux.
- Reference
  - https://microsoft.sharepoint.com/teams/MicrosoftLinux/SitePages/Home.aspx
  - https://linux-scripts.visualstudio.com/MSVPN-linux

## Quick start (with Docker)

1) [Install docker](https://docs.docker.com/install/linux/docker-ce/ubuntu/), and make sure your user has access to use it. (Add your local user to the docker group `sudo usermod -aG docker your-user`, and logout/login)
2) [Download this repository](https://linux-scripts.visualstudio.com/39fcc1e9-edaa-4da1-b205-f691a3068a5d/_apis/git/repositories/5bd2119e-0a64-4cb9-9c62-124b0e6534b3/Items?version%5D=master&%24format=zip): `wget https://linux-scripts.visualstudio.com/39fcc1e9-edaa-4da1-b205-f691a3068a5d/_apis/git/repositories/5bd2119e-0a64-4cb9-9c62-124b0e6534b3/Items?version%5D=master&%24format=zip`
3) Unzip this repository: `cd ~/Downloads && unzip MSVPN-linux.zip`
4) Copy the msftvpn-sample.yaml file to ~/.msftvpn.yaml
5) Edit the file and add a random UID for `host_uid`. You can generate one with `python -c 'import uuid; print(uuid.uuid1())'`. Also add your MSAD username under `msad_user`.
6) Copy `start.sh` to somewhere in your `$PATH`: `sudo cp start.sh /usr/local/bin/msftvpn`.

To use the VPN, run `start.sh` (from whatever name or file you copied it to). Use Ctrl+C to close the VPN connection.

## Install on your system without Docker

This can be useful, eg to integrate with a patched NetworkManager.

### OpenConnect with support for Palo Alto Networks GlobalProtect

OpenConnect **8.02** or higher is required.

If it's available in your distro, double-check that it also supports protocol `gp`. Do this with `openconnect --version` and look for `Supported protocols: ... gp` as shown below.

* Binary package on many distros is named `openconnect`, and is available with a sufficient version on Arch Linux, Ubuntu 19.10, and Fedora 30.

If it doesn't have `gp`, or the package is not available in your distro in the first place, follow the next steps to build it from source.

#### Source install on Debian/Ubuntu systems

* Download openconnect 8.02 (at a minimum) with gp support version from [here](ftp://ftp.infradead.org/pub/openconnect/openconnect-8.02.tar.gz)
  - sha256: 1ca8f2c279f12609bf061db78b51e5f913b3bce603a0d4203230a413d8dfe012

> [!NOTE]
> Grabbing the latest available version of OpenConnect may require minor tweaks to the paloalto.py script.

``` bash
~/$ sudo apt-get install build-essential gettext autoconf automake libproxy-dev libxml2-dev libtool vpnc-scripts pkg-config zlib1g-dev libgnutls28-dev
~/$ wget ftp://ftp.infradead.org/pub/openconnect/openconnect-8.02.tar.gz
~/$ sha256sum openconnect-8.02.tar.gz
~/$ tar zxvf openconnect-8.02.tar.gz
~/$ sha256sum openconnect-8.02.tar.gz
~/$ cd openconnect-8.02
~/$ ./configure
~/$ make
~/$ sudo make install && sudo ldconfig
~/$ sudo ln -s /usr/local/sbin/openconnect /usr/bin/openconnect
```

> [!NOTE]
> on Fedora *-dev packages are usually called *-devel

Make sure you have openconnect installed correctly in the $PATH
``` bash
~/$ openconnect --version
OpenConnect version v8.05
Using GnuTLS. Features present: TPM, TPMv2, PKCS#11, RSA software token, HOTP software token, TOTP software token, Yubikey OATH, System keys, DTLS, ESP
Supported protocols: anyconnect (default), nc, gp, pulse
~/$
```

### Chrome / Chromium browser

* This process should work with any browser which has a Selenium WebDriver, but the script is currently configured to use Chrome / Chromium with ChromeDriver. For Debian and Ubuntu:

``` bash
apt install chromium-browser chromium-chromedriver
```
Download the latest chromedriver from here - https://sites.google.com/a/chromium.org/chromedriver/ extract and copy it into ``` /usr/bin/chromedriver ```

### Configuration file

* Copy the sample ```msftvpn-sample.yaml``` to ```~/.msftvpn.yaml``` or ```$XDG_CONFIG_HOME/msftvpn/msftvpn.yaml``` and edit to match your preferences.
* Generate a new GUID for your host and set the value of the ```host_uid``` configuration variable. For example: ```python -c 'import uuid; print(uuid.uuid1())'```
* If the ```run_openconnect``` configuration variable is set to ```true```, the script will attempt to run OpenConnect using sudo. If you don't want this, and prefer to run OpenConnect manually, set the variable to ```false```.
* If the ```pipe_networkmanager``` configuration variable is set to ```true```, the script will output to stdout the key-value pairs required by network-manager-openconnect.

### MSFTVPN login script

* The script uses Python3 and depends on ```crypto```, ```packaging```, ```requests```, ```selenium.webdriver``` and ```yaml``` modules, beside stdlib bits. For Debian and Ubuntu:

``` bash
apt install python3-crypto python3-packaging python3 python3-requests python3-selenium python3-yaml
```

* Run the **paloalto.py** script with the privileges of your normal user. It needs to run a graphical browser interactively, so it is not meant for headless or pure CLI usage.
* link the script to a binary path and run it from the console.
  ``` bash
  ~/$ sudo ln -s /path/to/script/paloalto.py /usr/bin/msftvpn
  ~/$ sudo chmod +x /usr/bin/msftvpn
  ~/$ msftvpn
  ```
* The script will:
  1. Connect to MSFTVPN gateway and get a session URL to Microsoft's central authentication tool.
  2. Start a browser for manual web-based login, possibly requiring two-factor authentication.
  3. After a successful login, get a VPN token from MSFTVPN gateway.
    console output shoud look something like this:
    ``` bash 
    POST https://london.msftvpn-alt.ras.microsoft.com/ssl-vpn/getconfig.esp
    Connected to xxx.xxx.xxx.xxx:443
    SSL negotiation with london.msftvpn-alt.ras.microsoft.com
    Connected to HTTPS on london.msftvpn-alt.ras.microsoft.com
    Tunnel timeout (rekey interval) is 180 minutes.
    Idle timeout is 180 minutes.
    No MTU received. Calculated 1439 for SSL tunnel. No ESP keys received
    POST https://london.msftvpn-alt.ras.microsoft.com/ssl-vpn/hipreportcheck.esp
    Connected as xxx.xxx.xxx.xxx, using SSL, with ESP disabled

    ```
    the login has SSO (single sign on) that sticks within the same session (resets after reboot).
    don't close the console (**TODO:** make this work in the background and have a UI indicator for a successful connection)
    the session survives sleep (will restart automatically after wake).

  4. Optionally start OpenConnect with the previously-acquired token.
  Alternatively if you prefer to not start OpenConnect automatically, the script will print out the command line needed to start OpenConnect manually. This can then be copied to and run from another (possibly headless) system.

  5. Alternatively, if ```pipe_networkmanager``` is set to true in the config, it is possible to let
     network-manager-openconnect use this script automatically for authentication.
     Just edit /usr/lib/NetworkManager/VPN/nm-openconnect-service.name and change the auth-dialog
     option to point to the absolute path to **paloalto.py** (and restart the Gnome Shell session).
     Note that a still unreleased version of network-manager-openconnect with support for GP is
     required.
     It is also useful to know that NetworkManager supports split-dns, although it's not exposed via
     the GUI. Simply add ```dns=dnsmasq``` to the ```[main]``` section of **/etc/NetworkManager/NetworkManager.conf**
     and then add ```dns-search=corp.microsoft.com;``` under the ```[ipv4]``` section of the individual
     VPN config file, eg: **/etc/NetworkManager/system-connections/MSVPN.nmconnection**

**TODO:** script this procedure for a quick install and run.

### NixOS/Nixpkgs Workflow

Follow the directions from [how to setup your configuration file](#configuration-file) and then run:

```bash
./nix.paloalto.sh
```
This will download all system and python dependencies and execute the paloalto.py script.

* Information on Nixpkgs:
  * [Installation instructions for Nixpkgs.](https://nixos.org/nix/download.html).
  * [General information on Nixpkgs](https://nixos.org/nix/about.html).

### Disclaimer

These are **unofficial** instructions for running MSFTVPN under Linux.

~~MSIT~~ Core Services Engineering team does not provide Linux support, a Linux VPN client nor Linux instructions at this time. The tooling described below has been researched and compiled by volunteer Microsoft engineers who cannot and will not provide any kind of official support.

Using these instructions we have been able to successfully connect to MSFTVPN and run it. Because this is not an officially supported client, the gateway might disconnect you or completely stop accepting OpenConnect clients at any time.

The official GlobalProtect client automatically compiles an HIP (Host Intrusion Prevention) report and sends it to the server. This report contains information about client host's security features such as firewall, antivirus, disk encryption and patch level. There is no Microsoft-approved way to create such a report for a Linux host. We use OpenConnect in the hopes that MSFTVPN server will continue allowing connections from hosts which fail to provide a valid HIP report.

**This repository shall never contain instructions on how to provide a fake HIP report.** Please do not ask, nor attempt to add such instructions here. **If you decide to do this on your own anyway, you will be at the mercy of Microsoft's security teams.**