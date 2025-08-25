# Jenkins Remoting Project

This project demonstrates setting up **Jenkins Remoting** by connecting a Jenkins Controller to a remote Jenkins Agent using SSH on AWS EC2 instances. The setup distributes build loads securely across different machines and enforces node isolation for better security.

---

## 🚀 Project Overview
- **Controller Node:** Jenkins master running on an Ubuntu EC2 instance.  
- **Agent Node:** Remote Jenkins build agent running on another Ubuntu EC2 instance.  
- **Connection Method:** SSH with dedicated `jenkins` user and key-based authentication.  
- **Objective:** Run Jenkins jobs on remote agents instead of the controller to achieve workload distribution and isolation.

---

## 🛠️ Tech Stack
- **AWS EC2** (Ubuntu 22.04 LTS)  
- **Jenkins** (latest stable release)  
- **Java (OpenJDK 17)**  
- **SSH** (key-based authentication)  
- **Git**  

---

## 📂 Project Setup

### 1. AWS Infrastructure
- Created two EC2 instances:
  - **Controller Instance** (with port 22 & 8080 open to admin IP)
  - **Agent Instance** (with port 22 open only from Controller SG)
- Configured Security Groups to ensure secure SSH connections.

### 2. Jenkins Controller Setup
- Installed Java, Git, and Jenkins on the controller instance.
- Configured Jenkins and installed required plugins (SSH Build Agents).
- Disabled executors on the controller to enforce node isolation.

### 3. Agent Setup
- Installed Java and Git on the agent instance.
- Created a dedicated `jenkins` user with SSH access.
- Shared controller’s SSH key with the agent user for authentication.

### 4. Jenkins Remoting Configuration
- Added SSH credentials in Jenkins.
- Created a new node (`agent1`) in Jenkins with:
  - Remote root directory: `/home/jenkins`
  - Launch method: SSH using private IP
- Verified successful connection: **agent1 (online)**.

### 5. Test Job Execution
- Created a Freestyle and Pipeline job restricted to `agent1`.
- Console output confirmed jobs ran on the agent (`jenkins` user, agent hostname).

---

## 🔒 Security Best Practices
- Controller executors set to `0` (no jobs run on controller).
- Dedicated `jenkins` user on agent with limited privileges.
- Security Groups restrict SSH access (controller → agent only).
- SSH key-based authentication for secure communication.

---

## 📸 Screenshots
- EC2 Instances (Controller & Agent)
<img width="900" height="281" alt="now" src="https://github.com/user-attachments/assets/eeca45b7-65ca-4494-bddf-219829b99730" />


- Security Group rules
<img width="900" height="261" alt="83a8699b-fee1-4b51-b6a6-55e19eecec54" src="https://github.com/user-attachments/assets/ae7cda0a-abff-486f-bce2-21d927ab52da" />


- Jenkins Nodes page with **agent1 online**
<img width="900" height="300" alt="Screenshot from 2025-08-25 16-38-53" src="https://github.com/user-attachments/assets/e8dc04e4-db7d-4b84-916e-87a0af186ad9" />
<img width="900" height="300" alt="Screenshot from 2025-08-25 16-39-00" src="https://github.com/user-attachments/assets/d889e36a-2c29-4406-be1c-c92be06e5e55" />

- Console output of job running on agent
<img width="900" height="300" alt="Screenshot from 2025-08-25 16-47-06" src="https://github.com/user-attachments/assets/f50db7a1-abab-4bc9-98b4-37e0f84fee50" />


---

## ✅ Learning Outcomes
- Hands-on experience with **Jenkins remoting architecture**.  
- Setting up secure **controller-agent communication**.  
- Understanding **node isolation** and secure job execution.  
- Using **AWS EC2 + SSH** for distributed Jenkins builds.  

---

## 📌 Conclusion
This project successfully demonstrates Jenkins remoting by securely connecting a Jenkins controller with a remote agent over SSH, distributing jobs, and ensuring node isolation.


---
📘 **Read the full step-by-step blog here:**  
[Mastering Jenkins Remoting: Securely Distribute Builds Across Remote Nodes](https://visheshblog.hashnode.dev/day-64-mastering-jenkins-remoting-securely-distribute-builds-across-remote-nodes)
