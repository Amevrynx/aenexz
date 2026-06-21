# Week 1 — Assignment 2

# Task 1 — Your Machine's Network Identity

## Step 1: Network Information

| Item              | Your Value        |
| ----------------- | ----------------- |
| Computer Hostname | archlinux         |
| IPv4 Address      | 192.168.1.8       |
| Subnet Mask       | 255.255.255.0     |
| Default Gateway   | 192.168.1.1       |
| DNS Servers       | 8.8.8.8, 1.1.1.1  |
| MAC Address       | ****************  |
| Connection Type   | Wi-Fi             |

![hostname](https://github.com/Amevrynx/aenexz/blob/master/week-1_assignment2/host.png?raw=true)
 (I removed mac address for security concerns and public exposure)

---

## Step 2: Questions

### 1. What is your network's IP range?

IP Address:

```
192.168.1.8
```

Subnet Mask:

```
255.255.255.0
```

Network:

```
192.168.1.0/24
```

Usable Host Range:

```
192.168.1.1 – 192.168.1.254
```

---

### 2. How many devices could potentially be on your network?

A /24 network provides 256 addresses.

After excluding the network address and broadcast address, there are:

**254 usable hosts.**

---

### 3. Is your DNS server your router or an external service?

The system uses:

* Google DNS (8.8.8.8)
* Cloudflare DNS (1.1.1.1)

Therefore, DNS resolution is handled by external DNS services rather than the router.

---

### 4. Why does the MAC address matter?

A MAC address is a Layer 2 identifier used by switches to deliver frames inside the local network. It uniquely identifies a network interface and is visible before IP communication occurs.

---

# Task 2 — What Is Listening On Your Machine?

## Step 1: Open Ports

| Local Address | Port  | State  | Service             |
| ------------- | ----- | ------ | ------------------- |
| 0.0.0.0       | 22    | LISTEN | SSH                 |
| 0.0.0.0       | 80    | LISTEN | HTTP                |
| 0.0.0.0       | 81    | LISTEN | Nginx Proxy Manager |
| 0.0.0.0       | 4443  | LISTEN | Reverse Proxy HTTPS |
| 0.0.0.0       | 4533  | LISTEN | Docker Service      |
| 0.0.0.0       | 9000  | LISTEN | Portainer           |
| 0.0.0.0       | 9443  | LISTEN | Portainer HTTPS     |
| 0.0.0.0       | 19999 | LISTEN | Netdata             |
| 127.0.0.1     | 5432  | LISTEN | PostgreSQL          |
| 127.0.0.1     | 8125  | LISTEN | Monitoring Service  |
| 192.168.122.1 | 53    | LISTEN | DNS                 |
| 192.168.100.1 | 53    | LISTEN | DNS                 |

---

## Step 2: Questions

### 1. How many ports are in LISTEN state?

There are approximately **12 listening ports**.

---

### 2. Are any common ports present?

Yes.

| Port | Service    |
| ---- | ---------- |
| 22   | SSH        |
| 53   | DNS        |
| 80   | HTTP       |
| 5432 | PostgreSQL |

---

### 3. Is port 3389 (RDP) open?

No.

Remote Desktop Protocol is not exposed, reducing remote attack opportunities.

---

### 4. Is port 23 (Telnet) open?

No.

Telnet is insecure because it sends credentials in plaintext.

---

### 5. Difference between 0.0.0.0:PORT and 127.0.0.1:PORT?

#### 0.0.0.0:PORT

* Listens on all interfaces.
* Accessible from other devices.
* Larger attack surface.

#### 127.0.0.1:PORT

* Accessible only locally.
* Hidden from the network.
* More secure.

---

## Step 3: Top 10 common processes I daily use

| Process        | Purpose                    |
| -------------- | -------------------------- |
| systemd        | System initialization      |
| NetworkManager | Network management         |
| sshd           | SSH daemon                 |
| dockerd        | Docker daemon              |
| containerd     | Container runtime          |
| postgres       | PostgreSQL database        |
| libvirtd       | Virtual machine management |
| dnsmasq        | DNS and DHCP               |
| nginx          | Web server                 |
| netdata        | Monitoring service         |

![ps aux](https://github.com/Amevrynx/aenexz/blob/master/week-1_assignment2/ps.png?raw=true)

### Unknown Processes

No suspicious processes were identified. Most are expected for a Linux system running Docker, PostgreSQL, virtualization, and monitoring services.

---

# Task 3 — Scan Your Home Network

## Step 1: Network Range

Network:

```
192.168.1.0/24
```

Usable Range:

```
192.168.1.1 – 192.168.1.254
```

---

## Step 2: Ping Sweep Results

| IP Address  | Responded To Ping | Device Type    |
| ----------- | ----------------- | -------------- |
| 192.168.1.1 | Yes               | Router/Gateway |
| 192.168.1.2 | Yes               | Mobile         |
| 192.168.1.8 | Yes               | Laptop         |

![pingsweep image](https://github.com/Amevrynx/aenexz/blob/master/week-1_assignment2/pingsweep.png?raw=true)

**ifconfig results**
![ifconfig image1](https://github.com/Amevrynx/aenexz/blob/master/week-1_assignment2/ifconfig1.png?raw=true)

**i removed full ifconfig for security issues**

**netstat results**
![netstat image](https://github.com/Amevrynx/aenexz/blob/master/week-1_assignment2/nt2.png?raw=true)

---

## Step 3: Questions

### 1. How many devices responded?

Three devices responded.

1. Router (192.168.1.1)
2. mobile device at  192.168.1.2
3. Local laptop (192.168.1.8)

---

### 2. Did you find any unexpected devices?

No. All discovered devices were expected.

---

### 3. If an attacker got onto your Wi-Fi, how many devices could they potentially reach?

An attacker could communicate with every device on the network. At the time of the scan, three devices were reachable.

---

### 4. What is the security risk of having all devices on one flat network?

A flat network allows lateral movement. If one device becomes compromised, malware or an attacker could potentially spread to other devices. Network segmentation using VLANs or guest networks would improve security.

---

# Task 4 — Home Network Security Assessment

## 1. Network Overview

My home network uses the address range 192.168.1.0/24, providing 254 usable IP addresses. My laptop uses address 192.168.1.8 and connects through the gateway 192.168.1.1 over Wi-Fi. During the ping sweep, three active devices were discovered. In addition, the system hosts Docker containers and virtualization networks used for various services.

## 2. Open Ports & Services

Several ports are open and provide services including SSH (22), HTTP (80), Nginx Proxy Manager (81), Portainer (9000 and 9443), Netdata (19999), and PostgreSQL (5432). DNS services are used for virtualization networks. Ports 3389 (RDP) and 23 (Telnet) are closed, reducing unnecessary exposure.

## 3. Protocol Security

The network uses secure protocols such as HTTPS and SSH. DNS resolution uses Google DNS and Cloudflare DNS. PostgreSQL is bound to localhost, preventing external access. No Telnet services were found.

## 4. CIA Triad Analysis

### Confidentiality

Confidentiality is protected through encrypted protocols and password-protected Wi-Fi. Sensitive services like PostgreSQL are restricted to localhost.

### Integrity

Integrity is maintained through Linux permissions, Docker isolation, and controlled service access.

### Availability

Services remain continuously available through Docker and monitoring tools. However, many exposed ports increase the attack surface and may affect availability during attacks.

## 5. AAA Framework Analysis

### Authentication

Authentication is performed through Linux user accounts, SSH credentials, and application logins.

### Authorization

Linux permissions and Docker isolation control access to files and services.

### Accounting

System logs, journald, Docker logs, and Netdata monitoring provide activity records and auditing capability.

## 6. Recommendations

| # | Improvement                       | Why It Matters           | How To Do It                           |
| - | --------------------------------- | ------------------------ | -------------------------------------- |
| 1 | Disable unused services           | Minimize exposure        | Stop unnecessary containers and ports  |
| 2 | Use SSH key authentication        | Improve SSH security     | Disable password login                 |
| 3 | Keep software updated             | Patch vulnerabilities    | Use pacman updates regularly           |
| 4 | Implement VLANs or guest networks | Prevent lateral movement | Segment devices into separate networks |

## Conclusion

The network is relatively secure and uses modern protocols with no Telnet or RDP exposure. Several services are intentionally exposed for Docker and monitoring purposes. Additional hardening through firewall rules, network segmentation, and stronger authentication would further improve confidentiality, integrity, and availability.

---

# Task 5 — Bonus: Protocol Journal

| Time  | What I Did                  | Protocol Used  | Port  | Encrypted? | What Would An Attacker See? |
| ----- | --------------------------- | -------------- | ----- | ---------- | --------------------------- |
| 09:00 | Checked Gmail               | HTTPS          | 443   | Yes        | Encrypted traffic only      |
| 09:20 | Visited YouTube             | HTTPS          | 443   | Yes        | Encrypted traffic           |
| 09:45 | Used Google Search          | HTTPS          | 443   | Yes        | Encrypted traffic           |
| 10:00 | Updated Arch Linux packages | HTTPS          | 443   | Yes        | Package requests only       |
| 10:30 | Streamed music on Navidrome | HTTP           | 80    | No         | Traffic visible on LAN      |
| 11:00 | Accessed Portainer          | HTTPS          | 9443  | Yes        | Encrypted dashboard traffic |
| 11:15 | Viewed Netdata dashboard    | HTTP           | 19999 | No         | Monitoring information      |
| 11:30 | Connected through SSH       | SSH            | 22    | Yes        | Encrypted commands          |
| 12:00 | Resolved domain names       | DNS            | 53    | No         | Queried domains visible     |
| 12:30 | Visited GitHub              | HTTPS          | 443   | Yes        | Encrypted traffic           |
| 13:00 | Watched videos              | HTTPS          | 443   | Yes        | Encrypted traffic           |
| 13:30 | Accessed PostgreSQL locally | TCP/PostgreSQL | 5432  | Local Only | Not externally visible      |

---

# End of Submission
