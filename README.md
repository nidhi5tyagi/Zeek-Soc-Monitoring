# Zeek Network Traffic Analysis

## Project Overview

This project focuses on analyzing network traffic using **Zeek (formerly known as Bro)**, an open-source network security monitoring tool. The goal is to generate different types of network traffic, simulate potential security threats, analyze the generated logs, and create a report based on the findings.

---

## 1. Traffic Generation

To simulate network activity, perform the following tasks:

### a. Browsing Websites (HTTP/HTTPS Traffic)

Access websites using a browser or command-line tools:

```bash
curl http://www.example.com
curl https://www.google.com
```
![image](https://github.com/user-attachments/assets/32d22e22-7fe8-49c5-9b73-519828cef265)


### b. Performing DNS Queries

Run DNS resolution commands to generate DNS traffic:

```bash
dig www.example.com
nslookup www.google.com
```
![image](https://github.com/user-attachments/assets/49808dec-79fe-4d4c-b74f-37c0bd94a8ca)

### c. Using SSH for Remote Connections

Establish an SSH connection to generate traffic on port 22:

```bash
ssh user@<VM_IP>
```

![SSH Connection](screenshots/ssh_connection.png)

---

## 2. Simulating Malicious Activities

To test Zeek’s detection capabilities, simulate the following security threats:

### a. Running a Port Scan Using `nmap`

```bash
nmap -sS <VM_IP>
```

![image](https://github.com/user-attachments/assets/b9b463a8-58d8-4d08-bb1c-d913e11c11be)

### b. Generating a Suspicious HTTP Request

```bash
curl http://<VM_IP>/malicious-path
```

![image](https://github.com/user-attachments/assets/a7c4da90-b5a1-4a6a-a0ad-a7ea2e47c5db)
---

## 3. Log Analysis

Once Zeek captures traffic, analyze the logs stored in `/usr/local/zeek/logs/current/`. Key logs include:

### a. Connection Summaries (`conn.log`)

```bash
cat /usr/local/zeek/logs/current/conn.log
```
<img width="1617" alt="Screenshot 2025-02-21 at 3 51 36 PM" src="https://github.com/user-attachments/assets/b4509434-40e7-4635-9d44-862c902edd9a" />

### b. HTTP Transactions (`http.log`)

```bash
cat /usr/local/zeek/logs/current/http.log
```


### c. DNS Queries (`dns.log`)

```bash
cat /usr/local/zeek/logs/current/dns.log
```

<img width="1617" alt="Screenshot 2025-02-21 at 3 51 36 PM" src="https://github.com/user-attachments/assets/45e8713c-06f5-4a06-ba4a-a1811566a22c" />




### d. SSL/TLS Sessions (`ssl.log`)

```bash
cat /usr/local/zeek/logs/current/ssl.log
```


### e. Unusual Activity (`weird.log`)

```bash
cat /usr/local/zeek/logs/current/weird.log
```


---

---

## 4. Changing Zeek's Network Interface

If Zeek is listening on the wrong interface, modify the configuration in `zeekctl.cfg`:

```bash
sudo nano /usr/local/zeek/etc/node.cfg
```

Update the `interface` field to the correct network interface:

```
[zeek]
type=standalone
host=localhost
interface=enp0s8  # Change to the correct interface
```

Restart Zeek to apply changes:

```bash
sudo zeekctl deploy
```


---

## 5. Running Zeek and Capturing Logs

To manually start Zeek and capture live network traffic:

```bash
sudo zeek -i enp0s8
```

To restart Zeek with configuration settings:

```bash
sudo zeekctl stop
sudo zeekctl deploy
```


---


---

## Conclusion

This project demonstrates how Zeek can be used to monitor network traffic, detect suspicious activities, and analyze security logs. By following the outlined steps, you can effectively generate traffic, simulate attacks, and inspect logs for potential security threats.

---

