# Anonymity

+ ### MAC Address

 + **`ifconfig`**
        
        [Data Link Layer](), [Network Layer]()
        
        Default MAC Address : `n0:14:52:q6:30:d7`
    
        New MAC Address : `z5:82:12:s6:50:d0`. You can change to any.

        ```
        ifconfig

        ifconfig wlan0 down

        ifconfig wlan0 hw ether z5:82:12:s6:50:d0

        ifconfig wlan0 up

        ifconfig wlan0
        ```

 + **macchanger**

        [Data Link Layer]()

        Installation : `sudo apt install macchanger -y`

        ```
        sudo macchanger -r wlan0
        ```

+ ### Clearing Tracks

 + **`HISTSIZE`**

     ```
     echo $HISTSIZE

     export HISTSIZE=0
     ```

 + **`shred`**

     ```
     shred -zu /root/.bash_history
     ```
___


# Information Gathering

> Information gathering extends beyond mere data collection. It is a systematic process that involves acquiring, arranging, and evaluating data, facts, and knowledge from diverse sources using sophisticated information gathering tools.

+ **assetfinder**

  [Transport Layer](), [Network Layer]()

  Installation : `sudo apt install assetfinder -y`

  ```
  sudo assetfinder demowebsite.com
  ```

+ **finger**

  [Application Layer](), [Transport Layer]()

  Installation : `sudo apt install finger -y`

  ```
  sudo finger username

  sudo finger -s username

  sudo finger -p username
  ```

+ **netdiscover**

  [Data Link Layer](), [Network Layer]()
    
  Installation : `sudo apt install netdiscover -y`

  ```
  sudo netdiscover -i eth0 -r {IP}/24
  ```

+ **nmap**

    [Transport Layer](), [Network Layer]()
    
    Installation : `sudo apt install nmap -y`

    ```
    nmap 1.1.1.1
    // Scans all ports

    nmap -Pn 1.1.1.1
    // Scans TCP Ports
    -Pn		= Probes scan (Windows OS manuplates Firewall) used for Windows OS
    -p-		= Scan Entire TCP range (0-65535)
    -p 80		= Scans port 80
    -p 80,443,8080	= Scans ports 80,443,8080
    -p 1-65350	= Scans 1-65350 ports

    nmap -Pn -F 1.1.1.1
    -F		= Fast scan

    nmap -sV 1.1.1.1
    -sV		= Versions of Services

    nmap -sV -p139,445 192.168.0.1

    nmap -sV -T4 -O -F --version-light 192.168.0.1/24

    nmap -O 1.1.1.1
    -O		= Operating system

    nmap -v 1.1.1.1
    -v		= Scans limited 0-1000 ports

    nmap -Pn -sU 1.1.1.1
    -sU		= UDP Ports

    nmap -sC 1.1.1.1
    -sC		= (Gives detailed info of Versions of Services)

    nmap -T2 1.1.1.1
    -T2		= Scans Two Ports

    nmap -Pn 1.1.1.1 -oN test.txt
    -oN		= Output as Document
    -oX		= Output as XML format

    nmap -T4 -A -v 1.1.1.1

    nmap -sC demowebsite.com

    nmap -sC -p139,445 192.168.0.1

    nmap -sn 192.168.0.1/24

    nmap --script http-headers demowebsite.com

    nmap --script default,broadcast 192.168.0.1

    nmap --script "ssh-*" 192.168.0.1

    nmap --script banner demowebsite.com

    nmap --script dns-brute demowebsite.com
    ```

+ **rpcinfo**

    [Application Layer](), [Transport Layer]()
    
    Installation : `sudo apt install rpcinfo -y`
    
    ```
    rpcinfo -p 192.168.29.84

    rpcinfo -u 192.168.29.84 100024
    ```

+ **showmount**

    [Application Layer]()
    
    Installation : `sudo apt install showmount -y`

    ```
    showmount -d 127.0.0.1

    showmount -e 127.0.0.1
    ```

+ **whatweb**

    [Application Layer](), [Transport Layer]()
    
    Installation : `sudo apt install whatweb -y`

    ```
    whatweb demowebsite.com
    ```


+ **whois**

  [Transport Layer](), [Network Layer]()

  Installation : `sudo apt install whois -y`

+ **recon-ng**

  [Transport Layer](), [Network Layer]()

  Installation : `sudo apt install recon-ng -y`

+ **netcraft**

  [Transport Layer](), [Network Layer]()

  Installation : `sudo apt install netcraft -y`

+ **Angry-IP Scanner**

  [Transport Layer](), [Network Layer]()

  Installation : [Download](https://angryip.org/download)

+ **dig**

  [Transport Layer](), [Network Layer]()

  Installation : `sudo apt install dig -y`

+ **enum4linux**

  [Transport Layer](), [Network Layer]()

  Installation : `sudo apt install enum4linux -y`

___

# Denial of service (DOS)

+ **hping3**

  [Transport Layer](), [Network Layer]()

  Installation : `sudo apt install hping3 -y`

    ```
    hping3 -S 192.168.0.1 -p 80

    hping3 -S 192.168.0.1 -p ++79
    // ++ to increase port number

    hping3 -a 192.168.0.1 -S 192.168.0.2 -p ++20
    0.1=server || 0.2=attacker

    hping3 --udp -S 192.168.0.1 -p 80 --flood

    hping3 --icmp -S 192.168.0.1 -p 80 --flood

    hping3 --rand-source -S 192.168.0.1

    hping3 --ttl {value} -S {IP}

    hping3 --count {no.of packets} -S {ip add.}

    hping3 -scan 0-500 -S {IP}

    hping3 --flood -S --rand-source {IP}
    ```

___

# Exploitation

+ **smbclient**

  [Transport Layer](), [Network Layer]()

  Installation : `sudo apt install smbclient -y`

    ```
    smbclient -L \\\\192.168.0.1\\

    smbclient \\\\192.168.0.1\\tmp

    > help
    > dir
    ```

+ **smbmap**

  [Transport Layer](), [Network Layer]()

  Installation : `sudo apt install smbmap -y`

    ```
    smbmap -H 192.168.0.1
    ```

___

# MITM Attack

+ **arpspoof**

  [Transport Layer](), [Network Layer]()

  Installation : `sudo apt install arpspoof -y`

  ```
  echo 1 > /proc/sys/net/ipv4/ip_forward

  iptables -t nat -A PREROUTING -p tcp --destination-port 80 -j REDIRECT --to-port 8080

  arpspoof -i eth0 -t 192.168.1.218 -r 192.168.1.1
  // 192.168.1.218 : Hacking Machine
  // 192.168.1.1 : Hacking Machine Gateway (Router IP / Hotspot IP)

  sslstrip -l 8080

  nano sslstrip.log
  ```

+ **beef-xss**

  [Transport Layer](), [Network Layer]()

  Installation : `sudo apt install beef-xss -y`

  ```
  sudo beef-xss

  sudo beef-xss-stop
  ```

+ **ettercap**

  [Transport Layer](), [Network Layer]()

  Installation : `sudo apt install ettercap-graphical -y`

  ```
  1. Open **ettercap** application
  2. Click Tick icon
  3. Top Right - 3 dots  =>  Hosts  =>  Scan for Hosts
  4. Top Right - 3 dots  =>  Hosts  =>  Hosts list

  // ARP Poisoning Attack
  5. Top Right - Globe icon  =>  ARP Poisoning
  ```

___

# Wi-Fi

+ **`Monitor - Managed modes`**

  ```
  iwconfig

  ifconfig wlan0 down

  airmon-ng check kill

  iwconfig wlan0 mode monitor

  ifconfig wlan0 up

  iwconfig
  ```

+ **airodump**

  [Transport Layer](), [Network Layer]()

  Installation : `sudo apt install airodump -y`

+ **fluxion**

  [- Layer](), [- Layer]()

  Installation : `git clone https://www.github.com/FluxionNetwork/fluxion.git`

  ```
  cd fluxion

  ./fluxion.sh
  ```

+ **reaver**

  [- Layer](), [- Layer]()

  Installation : `sudo apt install reaver -y`

  ```
  reaver -i wlan0 -b 45:EF:46:87:D4:45 -S -v
  ```

+ **wash**

  [Transport Layer](), [Network Layer]()

  Installation : `sudo apt install wash -y`

  ```
  airmon-ng start wlan0

  wash -i wlan0mon
  ```

+ **wpa_wpa2**

___
# auto_bash_scripts

    + info_gathering.sh (nmap, assetfinder, smbmap, nikto)
    
___
# passwords_list

    + sql_payloads.txt

___
















Bettercap
Wireshark : Sniffing & Spoofing
Metasploit Framework
Social Engineering Toolkit
Aircrack-NG : Wi-Fi Cracker
Hydra : Crack passwds
John the Ripper : Crack passwds
Crunch : Generate passwords
Hash-Identifier & findmyhash
SQLMap
JoomScan & WPScan
HTTRACK
OWASP - ZAP
burpsuite
sqliv
nikto
dirbuster / dirb
maltego - community edition
whatweb
tracetoute
proxychains
