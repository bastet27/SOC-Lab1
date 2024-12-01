# SOC Automation Lab Project  

## Table of Contents  

| Description                         |
|-------------------------------------|
| [Research and Getting Ready](#research-and-getting-ready) |
| [Visualization](#visualization)            |
| [Installing Wazuh](#installing-wazuh)            |
| -                  | [4 ]            |
| -                  | [5 ]            |


### :green_book: Introduction  

I’m excited to embark on a journey to build a fully functional **SOC (Security Operations Center) Automation Lab**, following the guide outlined in this [write-up](https://medium.com/@jashankhaira52/day-1-building-your-soc-automation-lab-an-introduction-and-overview-c1825642369e). This project is an opportunity to gain hands-on experience with incident detection, response, and automation, using tools commonly found in SOC environments.  

My lab will be set up using the **AWS Free Tier**, which makes cloud-based solutions accessible and scalable without requiring expensive hardware. This approach allows me to focus on the critical elements of building, automating, and scaling SOC workflows.  

The lab will utilize several powerful tools:  
- **[Wazuh](https://documentation.wazuh.com/current/)**: A security information and event management (SIEM) platform for real-time threat detection.  
- **[The Hive](https://thehive-project.org/documentation/)**: A case management tool for tracking and resolving incidents.  
- **[Shuffle](https://shuffler.io/docs/)**: A security orchestration, automation, and response (SOAR) platform to automate incident workflows.  
- **[Elasticsearch](https://www.elastic.co/guide/en/elasticsearch/reference/current/index.html)**: A log storage and retrieval solution.  
- **[Kibana](https://www.elastic.co/guide/en/kibana/current/index.html)**: A visualization tool for analyzing and exploring log data.  

### 🎯 Goals for the SOC Lab Project  
I plan to:  
- Set up a cloud-based SOC environment using AWS Free Tier.  
- Integrate Wazuh, The Hive, and Shuffle to detect and respond to threats.  
- Automate incident response workflows for efficiency and scalability.  
- Document the process to build a portfolio-ready project for showcasing my skills.  

### ☁️ Why AWS Free Tier?  
Cloud-based labs are a game-changer for accessibility and scalability. With AWS Free Tier, I can:  
- Build and test my lab without high upfront costs.  
- Scale resources as my project grows.  
- Access my lab from anywhere with an internet connection.  

This SOC Automation Lab will help me gain real-world cybersecurity skills while laying the foundation for future growth and advanced integrations. Stay tuned as I document this exciting process and share my progress! 🚀  

## Research and Getting Ready

### :green_book: Tasks Completed  

- **GitHub Account**: I already have a GitHub account set up, where I document my progress and share write-ups for my cybersecurity projects.  
- **Documentation Platform**: My GitHub serves as the primary platform for showcasing my work and skills to potential employers.  
- **Research**: Began researching the tools I’ll use in this project by reviewing their official documentation.  

### :toolbox: Tools Overview  

- **[Wazuh](https://documentation.wazuh.com/current/)**  
  Wazuh is an open-source SIEM and XDR platform that provides:  
  - Real-time threat detection and response.  
  - Log management and security analytics.  
  - Endpoint detection capabilities, ensuring comprehensive visibility into security events.  

- **[The Hive](https://thehive-project.org/documentation/)**  
  The Hive is an incident response and case management system designed to:  
  - Organize and track security incidents.  
  - Assign cases for investigation, making incident management more efficient.  
  - Provide integration with other tools like Wazuh and Shuffle for a cohesive workflow.  

- **[Shuffle](https://shuffler.io/docs/)**  
  Shuffle is a lightweight SOAR platform that allows for:  
  - Automation of incident response workflows.  
  - Integration with tools like Wazuh and The Hive for seamless response actions.  
  - Customizable workflows to streamline repetitive tasks, improving SOC efficiency.  

## Visualization 

### :green_book: Tasks Completed  

1. **Created a Workflow Diagram**  
   Using [draw.io](https://app.diagrams.net/), I designed a workflow diagram to visualize the data flow across the SOC automation lab. Each step and interaction is color-coded. 

### :art: Workflow Diagram  

![SOC Automation Workflow Diagram](https://github.com/user-attachments/assets/34633435-6771-4a34-b1c7-3db66769ac27)

### Step-by-Step Breakdown of the Workflow  

#### **💖 Pink: Event Flow**  
- **💖 Step 1: Send Events**  
  - **Windows 10 Client (Wazuh Agent)** sends event logs to the **Wazuh Manager** via the router. This step captures endpoint activity for analysis.  
- **💖 Step 2: Receive Events**  
  - **Wazuh Manager** receives the event logs and analyzes them. It triggers alerts when predefined conditions, such as detecting specific threats, are met.  

#### **🟦 Teal: Alert Transmission**  
- **🟦 Step 3: Send Alerts**  
  - **Wazuh Manager** sends triggered alerts to **Shuffle** for further processing. This step transitions event data into actionable intelligence.  
- **🟦 Step 5: Send Alerts to The Hive**  
  - Once enriched, **Shuffle** sends these alerts to **The Hive**, a case management system, for logging and tracking.  

#### **💚 Green: Enrich IoCs**  
- **💚 Step 4: Enrich IoCs**  
  - **Shuffle** enriches the alerts by performing Open Source Intelligence (OSINT) gathering. This enhances the understanding of Indicators of Compromise (IoCs), providing valuable context for incident response.  

#### **🧡 Orange: SOC Analyst Notification**  
- **🧡 Step 6: Send Email to SOC Analyst**  
  - **Shuffle** sends an email notification to the **SOC Analyst**, detailing the incident and prompting action.  
- **🧡 Step 7: Send and Receive Email**  
  - The **SOC Analyst** reviews the email and responds by selecting a containment or remediation action based on the provided information.  

#### **💙 Blue: Response Action**  
- **💙 Step 8: Perform Response Action**  
  - The analyst’s response is sent back through **Shuffle**, which processes the response and forwards it to the **Wazuh Manager**. The **Wazuh Manager** then issues commands to the **Windows 10 Client** to execute the remediation action.  

### Data Flow Summary 📊  

| Color | Flow                                                                                 | Purpose                                                |
|-------|--------------------------------------------------------------------------------------|--------------------------------------------------------|
| 💖    | **Event Flow**: Windows 10 → Wazuh Manager                                           | Captures and analyzes logs from the endpoint.         |
| 🟦    | **Alert Transmission**: Wazuh Manager → Shuffle → The Hive                           | Converts events into actionable alerts for tracking.  |
| 💚    | **Enrich IoCs**: Data enrichment through Shuffle                                     | Enhances understanding of threats and IoCs.           |
| 🧡    | **SOC Analyst Notification**: Shuffle → SOC Analyst                                  | Notifies analysts of incidents needing attention.     |
| 💙    | **Response Action**: SOC Analyst → Shuffle → Wazuh Manager → Windows 10              | Executes remediation actions based on analyst input.  |

The workflow diagram is a critical tool in understanding how data flows through the SOC automation system. Each color-coded step represents a distinct function, from capturing event logs to enriching data and responding to incidents. The purpose of the diagram is to clearly visualize the roles of each component and their interactions, ensuring the SOC system operates seamlessly. This serves as a reference point for implementing and configuring the lab, allowing for efficient detection, enrichment, and response processes.

## Installing Wazuh

### :green_book: Tasks Completed  

1. **Launched an EC2 Instance**  
   - Used **AWS EC2** instead of DigitalOcean for hosting Wazuh, leveraging AWS's **Free Tier** to minimize costs while gaining access to a scalable and reliable platform.  
   - Configured the instance with appropriate security group rules for SSH, HTTP, and HTTPS access.  

2. **Installed Wazuh**  
   - Successfully installed Wazuh using the official installation script, bypassing a minor compatibility check issue.  

### :computer: Setting Up the EC2 Instance  

#### **Instance Configuration**  
- **Instance Type**: t2.micro (Free Tier eligible; 1 vCPU, 1GB RAM).  
- **AMI**: Ubuntu 22.04 LTS.  
- **Storage**: 30GB General Purpose SSD (gp2).  
- **Security Group Rules**:  
  | **Rule** | **Type**  | **Protocol** | **Port Range** | **Source**         |  
  |----------|-----------|--------------|----------------|---------------------|  
  | 1        | SSH       | TCP          | 22             | My IP (`<Your_IP>`)|  
  | 2        | HTTPS     | TCP          | 443            | Anywhere (0.0.0.0/0)|  
  | 3        | HTTP      | TCP          | 80             | Anywhere (0.0.0.0/0)|  

#### **Why AWS Instead of DigitalOcean?**  
- **Cost-Effective**: AWS's **Free Tier** allowed me to run a t2.micro instance at no cost for the first 12 months.  
- **Scalability**: AWS provides easy scalability for future needs as the SOC lab grows.  
- **Global Infrastructure**: AWS’s wide range of data centers offers better performance and reliability.  

#### Wazuh Instance is Running

<img width="1064" alt="wazuh-aws-instance-running" src="https://github.com/user-attachments/assets/b30cd223-3de6-4f1a-8c90-b22b2efbf266">


#### **Connecting to the Instance**  
- **SSH Command**:  
  ```
  ssh -i "wazuh-key.pem" ubuntu@<Your_EC2_Public_IP>
  ```

- **Updating the System**:  
  After connecting, updated and upgraded the system packages to ensure compatibility:  
  ```
  sudo apt-get update && sudo apt-get upgrade -y
  ```

### :wrench: Installing Wazuh  

#### **Download and Run the Installation Script**  
- Downloaded the Wazuh installation script and executed it with a compatibility check bypass:  
  ```
  curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh && sudo bash ./wazuh-install.sh -a --ignore-check
  ```

#### **Post-Installation Notes**  
- Saved the admin credentials displayed after the installation for accessing the Wazuh dashboard.  
- Verified installation logs to ensure no errors:  
  ```
  cat /var/log/wazuh-install.log
  ```

### :chart_with_upwards_trend: Accessing the Wazuh Dashboard  

#### **Access URL**  
- Accessed the Wazuh dashboard by entering the EC2 instance’s public IP in a web browser:  
  ```
  https://<Your_EC2_Public_IP>
  ```

#### **Security Warning**  
- Clicked **Advanced > Proceed** to bypass the warning caused by the self-signed certificate.  

#### **Login**  
- Used the admin credentials saved during the installation to log in to the dashboard.  

### Summary  

For hosting Wazuh, I chose **AWS EC2** instead of DigitalOcean, primarily because of the **Free Tier**, which allowed me to deploy a t2.micro instance at no cost. AWS’s scalability and global infrastructure provide a robust platform for building the SOC Automation Lab. This step involved configuring the instance, setting up security group rules, and successfully installing Wazuh. The Wazuh dashboard is now operational, serving as the foundation for monitoring and managing security events in the lab. 🚀  
