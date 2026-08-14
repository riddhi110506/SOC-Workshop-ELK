# ELK Stack Setup

> **Ubuntu Desktop – ELK Server**

This guide explains the setup of the ELK Stack on Ubuntu Desktop.

The ELK Stack consists of:

- Elasticsearch
- Logstash
- Kibana

---

## Step 1: Update Ubuntu

Open the Ubuntu terminal and run the following commands:

```bash
sudo apt update
sudo apt upgrade -y
```

---

## Step 2: Install Required Packages

Install the required packages:

```bash
sudo apt install apt-transport-https wget curl gnupg unzip -y
```

---

## Step 3: Import the Elastic GPG Key

Run the following command:

```bash
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | \
sudo gpg --dearmor -o /usr/share/keyrings/elasticsearch-keyring.gpg
```

---

## Step 4: Add the Elastic Repository

Add the Elastic 8.x repository:

```bash
echo "deb [signed-by=/usr/share/keyrings/elasticsearch-keyring.gpg] https://artifacts.elastic.co/packages/8.x/apt stable main" | \
sudo tee /etc/apt/sources.list.d/elastic-8.x.list
```

---

## Step 5: Update Package List

Update the package list:

```bash
sudo apt update
```

---

## Step 6: Install Elasticsearch

Install Elasticsearch:

```bash
sudo apt install elasticsearch -y
```

---

## Step 7: Enable and Start Elasticsearch

Run the following commands:

```bash
sudo systemctl daemon-reload
sudo systemctl enable elasticsearch
sudo systemctl start elasticsearch
```

### Verify Elasticsearch

Check the Elasticsearch service:

```bash
sudo systemctl status elasticsearch
```

### Expected Result

The service should display:

```text
Active: active (running)
```

---

## Step 8: Install Kibana

Install Kibana:

```bash
sudo apt install kibana -y
```

### Enable and Start Kibana

Run:

```bash
sudo systemctl enable kibana
sudo systemctl start kibana
```

### Verify Kibana

Check the Kibana service:

```bash
sudo systemctl status kibana
```

### Expected Result

The service should display:

```text
Active: active (running)
```

---

## Step 9: Install Logstash

Install Logstash:

```bash
sudo apt install logstash -y
```

### Enable and Start Logstash

Run:

```bash
sudo systemctl enable logstash
sudo systemctl start logstash
```

### Verify Logstash

Check the Logstash service:

```bash
sudo systemctl status logstash
```

### Expected Result

The service should display:

```text
Active: active (running)
```

---

## Step 10: Start All ELK Services

Restart all three ELK services:

```bash
sudo systemctl restart elasticsearch
sudo systemctl restart kibana
sudo systemctl restart logstash
```

### Verify All Services

Run:

```bash
sudo systemctl status elasticsearch
sudo systemctl status kibana
sudo systemctl status logstash
```

### Expected Result

All three services should display:

```text
Active: active (running)
```

---

## Step 11: Get the Elasticsearch Password

Generate the Elasticsearch password for the `elastic` user:

```bash
sudo /usr/share/elasticsearch/bin/elasticsearch-reset-password -u elastic
```

Save the generated password.

Create a password file:

```bash
nano password.txt
```

Paste the generated password into the file.

> **Important:** Do not upload `password.txt` or any password to GitHub.

---

## Step 12: Verify Elasticsearch

Run the following command:

```bash
sudo curl --cacert /etc/elasticsearch/certs/http_ca.crt \
-u elastic:<PASSWORD> \
https://localhost:9200
```

Replace `<PASSWORD>` with the Elasticsearch password generated in Step 11.

### Expected Result

You should receive a response similar to:

```json
{
  "name": "ubuntu",
  "cluster_name": "elasticsearch",
  "version": {
    "number": "8.x"
  },
  "tagline": "You Know, for Search"
}
```

---

## Step 13: Access Kibana

Open a web browser and navigate to:

```text
http://localhost:5601
```

> **Note:** Do not select **Configure manually** during the initial setup.

### Generate Kibana Enrollment Token

Open the Ubuntu terminal and run:

```bash
sudo /usr/share/elasticsearch/bin/elasticsearch-create-enrollment-token -s kibana
```

Copy the complete enrollment token.

Paste the enrollment token into the Kibana browser page.

### Login to Kibana

Use:

```text
Username: elastic
Password: <Elasticsearch password>
```

Use the password saved during Step 11.

### Generate Kibana Verification Code

Run:

```bash
sudo /usr/share/kibana/bin/kibana-verification-code
```

The verification code will be displayed in the terminal.

### Verify Kibana

Run:

```bash
sudo systemctl status kibana
```

The Kibana service should be running.

---
Webpage of kibana should open in Ubuntu

