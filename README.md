# 🚀 DevOps Monitoring & Observability Stack using Grafana, Prometheus & Loki

#### **Author:** Vaibhav Gautam  
#### **Project Type:** End-to-End Observability Implementation  
#### **Tools Used:** Grafana • Prometheus • Loki • Linux • Bash • Slack Alerts

---

## 📌 **Project Objective**

Modern systems require deep visibility into **metrics**, **logs**, and **system behavior** in real time.  
This project demonstrates how to build a **complete monitoring and observability stack** from scratch using industry-standard open-source tools.

The goal is to:

- Monitor application & system metrics
- Aggregate and analyze logs centrally
- Visualize system behavior with dashboards
- Trigger real-time alerts to Slack when thresholds are breached

---

## 🧱 **Architecture Overview**

<img width="963" height="832" alt="PortNumbers (1)" src="https://github.com/user-attachments/assets/0e310430-0c2e-4f8c-98a5-a87bec410fb3" />


---


### 🛠**1. Setting Up the Monitoring Environment**

### A. *Grafana*

#### 1. Launch an instance**
<img width="1919" height="1020" alt="1" src="https://github.com/user-attachments/assets/44c2a1f3-efb6-4a2b-a76f-174f9c215712" />

#### **2. SSH into the instance**
<img width="1919" height="1014" alt="2" src="https://github.com/user-attachments/assets/a2136c76-3325-4ff4-9910-febb4a1ab968" />

#### **3. Download the script ( grafana-setup.sh )**
```grafana-setup.sh
#!/bin/bash

# Grafana Enterprise Installation Script
# Standard paths: /etc/grafana (config), /var/lib/grafana (data)
# Version: 12.2.1

set -e

# Variables
GRAFANA_VERSION="12.2.1"
DOWNLOAD_URL="https://dl.grafana.com/grafana-enterprise/release/${GRAFANA_VERSION}/grafana-enterprise_${GRAFANA_VERSION}_18655849634_linux_amd64.deb"
DEB_FILE="grafana-enterprise_${GRAFANA_VERSION}_18655849634_linux_amd64.deb"
SERVICE="grafana-server"

# Update system
sudo apt update && sudo apt upgrade -y

# Install dependencies
sudo apt-get install -y adduser libfontconfig1 musl

# Download package
wget "${DOWNLOAD_URL}"

# Install package
sudo dpkg -i "${DEB_FILE}"

# Reload, enable, and start service
sudo systemctl daemon-reload
sudo systemctl enable "${SERVICE}"
sudo systemctl start "${SERVICE}"

echo "Grafana Enterprise installed successfully!"
echo " - Config: /etc/grafana/grafana.ini"
echo " - Data: /var/lib/grafana/"
echo " - Service: systemctl status ${SERVICE}"
echo "Access Grafana UI at http://GrafanaIP:3000 (default admin/admin)"
```
#### or use raw link
```raw link
sudo wget https://raw.githubusercontent.com/vaibhavgautam5157/DevOps-Project-Monitoring-and-Observability/refs/heads/main/grafna-setup.sh
```
```
# make it executable
chmod +x grafana-setup.sh
./grafana-setup.sh
```

#### **4. Access the IP on port 3000**
<img width="1919" height="1021" alt="3" src="https://github.com/user-attachments/assets/8b1c9244-0433-4438-87a0-7d176e43bb4a" />
<img width="1919" height="1011" alt="4" src="https://github.com/user-attachments/assets/3092f26d-ca16-41a9-aeee-c87e8a119407" />


### B. *Prometheus*

#### **1. Launch an instance**
<img width="1919" height="1018" alt="5" src="https://github.com/user-attachments/assets/d78fe65e-5c18-40dc-86b5-17bdd9e6f852" />

#### **2. Download the scripts ( prometheus-setup.sh )**
```
sudo https://raw.githubusercontent.com/vaibhavgautam5157/DevOps-Project-Monitoring-and-Observability/refs/heads/main/prometheus-setup.sh
```

```
# make it executable
chmod +x prometheus-setup.sh
./prometheus-setup.sh
```

#### **3. Adding the nodes**
**WebsiteTest-main.sh**
```
sudo https://raw.githubusercontent.com/vaibhavgautam5157/DevOps-Project-Monitoring-and-Observability/refs/heads/main/WebsiteTest-main.sh
```

```
# make it executable
chmod +x WebsiteTest-main.sh
./WebsiteTest-main.sh
```

**WebsiteTest-payment.sh**
```
https://raw.githubusercontent.com/vaibhavgautam5157/DevOps-Project-Monitoring-and-Observability/refs/heads/main/WebsiteTest-payment.sh
```

```
# make it executable
chmod +x WebsiteTest-payment.sh
./WebsiteTest-payment.sh
```



#### **4. Access the IP on port 9090**
<img width="1919" height="1016" alt="6" src="https://github.com/user-attachments/assets/69f13bc9-dd84-4757-9c91-a74fff928d19" />
<img width="1919" height="1019" alt="7" src="https://github.com/user-attachments/assets/28634aeb-2b78-4b42-88fb-9ad287bdfeca" />

#### Metrics
<img width="1919" height="1016" alt="8" src="https://github.com/user-attachments/assets/e2457c3f-b821-47a9-8bb2-b7e27123765b" />


---

### 🛠**2. *Loki* and *Web-server* setup**

#### **1. Launch an instance (loki) and Download the script ( loki-setup.sh )**
```
sudo https://raw.githubusercontent.com/vaibhavgautam5157/DevOps-Project-Monitoring-and-Observability/refs/heads/main/loki-setup.sh
```

```
# make it executable
chmod +x loki-setup.sh
./loki-setup.sh
```

#### **2. Launch an instance (web-01) and Download the script ( webnode-setup.sh )**
```
https://raw.githubusercontent.com/vaibhavgautam5157/DevOps-Project-Monitoring-and-Observability/refs/heads/main/webnode-setup.sh
```

```
# make it executable
chmod +x webnode-setup.sh
./webnode-setup.sh
```

#### **3.Access the IP on port 5000**
<img width="1919" height="1013" alt="9" src="https://github.com/user-attachments/assets/6c67af55-b79b-4d4a-8efd-3a1297b096ae" />
<img width="1919" height="1017" alt="10" src="https://github.com/user-attachments/assets/5e9defed-4ade-433b-9388-bd2f374317c6" />

---


### 🖥️**3. Connecting Grafana and Prometheus**

Grafana was configured with:

-  **Prometheus as Metrics Data Source**
- **Loki as Logs Data Source**
  
**This allows correlated analysis of logs and metrics in one dashboard.**


<img width="1919" height="1012" alt="18" src="https://github.com/user-attachments/assets/ea57e464-beaa-4b23-88c0-39baea0f8575" />

<img width="1919" height="1016" alt="Screenshot 2025-12-30 182337" src="https://github.com/user-attachments/assets/a1f3e6dc-f1ca-44d5-a609-01594aa76dd9" />

<img width="1919" height="1012" alt="15" src="https://github.com/user-attachments/assets/0fe7ca59-e983-4447-9a61-55d49a8d813c" />
<img width="1899" height="994" alt="16" src="https://github.com/user-attachments/assets/0464c83b-8bf5-49a8-bcb4-476414f69960" />
<img width="1919" height="1005" alt="17" src="https://github.com/user-attachments/assets/9f736c89-a7b0-44ec-be3b-7c14f1bbd8de" />

---

### 📈**4. Querying & Visualization**

**PromQL queries were used to visualize:**

- **Request rate**
- **System load**
- **Response metrics**

**Dashboards created:**

- **Graph Panels**
- **Stacked Bar Graphs**
- **Real-time metrics visualization**

<img width="1907" height="1015" alt="20" src="https://github.com/user-attachments/assets/71068aff-8b69-47a5-8875-421fb55b8b27" />

<img width="1919" height="1035" alt="21" src="https://github.com/user-attachments/assets/da17ec06-06fa-4807-bcc6-161af7ccd5e5" />

#### Stacked Bar Graph
<img width="1919" height="1018" alt="22" src="https://github.com/user-attachments/assets/04cfd1ff-b1da-416f-b703-48db2d608215" />


---


### 🚨**4. Slack Alert Integration (Alerting System)**

To simulate real production monitoring:

- **Alert rules created in Grafana**
- **Slack webhook integrated**
- **Notifications triggered when thresholds exceeded**

**This demonstrates incident awareness and alert management.**


<img width="1919" height="1015" alt="27" src="https://github.com/user-attachments/assets/753a50aa-9344-4987-ad4b-93bd152cf3ed" />


<img width="1919" height="1016" alt="29" src="https://github.com/user-attachments/assets/48dc7709-b6cb-4d07-a6a5-61862d555373" />
<img width="1919" height="1018" alt="30" src="https://github.com/user-attachments/assets/5e45ca7b-f4df-4047-842c-674c5e8c15cd" />

<img width="1919" height="1002" alt="31" src="https://github.com/user-attachments/assets/52e1a06b-19ff-40f2-865c-0231b26c309e" />
<img width="1916" height="1014" alt="32" src="https://github.com/user-attachments/assets/0a0cef13-9cac-4e15-9cd8-3210bd5235df" />

<img width="1918" height="1010" alt="33" src="https://github.com/user-attachments/assets/41601917-cf17-4a39-9960-b5aea5e4545f" />
<img width="1919" height="1013" alt="34" src="https://github.com/user-attachments/assets/d6225b04-d0f0-4ce7-8cc5-59175b2aea99" />

<img width="1919" height="999" alt="36" src="https://github.com/user-attachments/assets/e9b0e3ed-76dc-48e6-aaba-133e6d2ac010" />
<img width="1919" height="1012" alt="37" src="https://github.com/user-attachments/assets/c6007560-1159-43f3-b3c8-958c0cd5329b" />
























