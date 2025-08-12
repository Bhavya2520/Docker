# Jenkins Zero to Hero 🚀

Learn **Jenkins** from scratch — starting from installation to building **end-to-end CI/CD pipelines**.  
You will install Jenkins on an AWS EC2 instance, configure Docker as an agent, set up CI/CD pipelines, and deploy applications to Kubernetes.

---

## 📌 Prerequisites

- **AWS Account** with access to launch EC2 instances.
- Basic understanding of **Linux commands**.
- Security group permissions to open required ports.
- Familiarity with **Docker** and **CI/CD concepts** (optional but helpful).

---

## 1️⃣ Launch an AWS EC2 Instance

1. Go to **AWS Console** → **EC2** → **Instances** → **Launch Instances**.
2. Choose **Ubuntu** as your OS.
3. Select an appropriate instance type (e.g., `t2.medium`).
4. Configure **Security Group**:
   - Allow inbound **Custom TCP** on port `8080` (for Jenkins access).
   - Alternatively, allow **All Traffic** (⚠ not recommended for production).

![AWS EC2 Instance](https://user-images.githubusercontent.com/43399466/215974891-196abfe9-ace0-407b-abd2-adcffe218e3f.png)

---

## 2️⃣ Install Java (Jenkins Requirement)

```bash
sudo apt update
sudo apt install openjdk-17-jre
```

Verify installation:

```bash
java -version
```

---

## 3️⃣ Install Jenkins

```bash
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee   /usr/share/keyrings/jenkins-keyring.asc > /dev/null

echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]   https://pkg.jenkins.io/debian binary/ | sudo tee   /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt-get update
sudo apt-get install jenkins
```

---

## 4️⃣ Configure AWS Security Group for Jenkins Access

- Go to **EC2 > Instances > Select Your Instance**.
- Click **Security** → **Security Groups**.
- Add inbound rule for:
  - **Custom TCP** on port `8080`.
  - Or **All traffic** (⚠ not recommended).

![Security Group](https://user-images.githubusercontent.com/43399466/215975712-2fc569cb-9d76-49b4-9345-d8b62187aa22.png)

---

## 5️⃣ Access Jenkins

- Visit:  
  `http://<EC2-Public-IP>:8080`
- Get the Jenkins Admin password:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

- Enter the password in the Jenkins setup page.
- Click **Install suggested plugins**.
- Create the first admin user (optional but recommended).

![Jenkins Setup](https://user-images.githubusercontent.com/43399466/215959008-3ebca431-1f14-4d81-9f12-6bb232bfbee3.png)

---

## 6️⃣ Install Docker Pipeline Plugin

1. Go to **Manage Jenkins → Manage Plugins**.
2. Search for **Docker Pipeline**.
3. Install and restart Jenkins.

![Docker Pipeline Plugin](https://user-images.githubusercontent.com/43399466/215973898-7c366525-15db-4876-bd71-49522ecb267d.png)

---

## 7️⃣ Install Docker on EC2

```bash
sudo apt update
sudo apt install docker.io
```

---

## 8️⃣ Give Jenkins & Ubuntu Users Docker Permissions

```bash
sudo su -
usermod -aG docker jenkins
usermod -aG docker ubuntu
systemctl restart docker
```

---

## 9️⃣ Restart Jenkins

```bash
http://<EC2-Public-IP>:8080/restart
```
