# Wazuh-XDR-and-SIEM-Implementation

![Screenshot_2024-05-28_19_33_25](https://github.com/ELPatrinum/Wazuh-XDR-and-SIEM-Implementation/assets/121964622/cdd6c38b-c1d2-4b49-9151-920cb0180db8)
![Screenshot_2024-05-28_19_35_12](https://github.com/ELPatrinum/Wazuh-XDR-and-SIEM-Implementation/assets/121964622/4444a8ab-6899-4207-ae0e-6a1f5e68ca7e)
![Screenshot_2024-05-28_19_44_32](https://github.com/ELPatrinum/Wazuh-XDR-and-SIEM-Implementation/assets/121964622/787a73ef-e036-46c5-8290-a36c67c04792)
![Screenshot_2024-05-28_19_44_57](https://github.com/ELPatrinum/Wazuh-XDR-and-SIEM-Implementation/assets/121964622/27e0f784-b5a8-4cdf-a4db-74e52f5ff893)
![Screenshot_2024-05-28_19_46_19](https://github.com/ELPatrinum/Wazuh-XDR-and-SIEM-Implementation/assets/121964622/debaf53b-572b-4bbf-ac09-171ef3d6d61e)
![Screenshot_2024-05-28_19_47_19](https://github.com/ELPatrinum/Wazuh-XDR-and-SIEM-Implementation/assets/121964622/49a85be6-3559-48a1-bdab-f9792bb4d167)
![Screenshot_2024-05-28_19_46_36](https://github.com/ELPatrinum/Wazuh-XDR-and-SIEM-Implementation/assets/121964622/130a934e-4c93-47fe-9273-00936bb40ec0)


Manage and Monitor a Windows and a Linux machines simultaneously using Wazuh

This project involved the deployment and configuration of Wazuh to enhance the organization's cybersecurity posture through its extended detection and response (XDR) capabilities and comprehensive Security Information and Event Management (SIEM) solution. The primary objectives were to:
- **Deploy Wazuh**: Set up and configure Wazuh on multiple endpoints and servers to ensure broad coverage across the network.
- **Implement Active XDR Protection**: Integrate Wazuh's XDR features to provide proactive threat detection, investigation, and automated response capabilities.
- **Comprehensive SIEM Solution**: Utilize Wazuh's SIEM functionalities to collect, analyze, and correlate security events from various sources, enabling real-time monitoring and incident management.
- **Enhance Security Monitoring**: Establish a centralized monitoring system to improve visibility into security incidents and streamline the response process.
- **Compliance and Reporting**: Ensure compliance with industry standards and regulations by generating detailed reports and maintaining an audit trail of security events.
---------------------------------------------------------------------------------------------------------------------------------------------------
Wazuh is an open-source security platform that provides comprehensive threat detection, visibility, compliance, and incident response capabilities. It integrates various security functions into a unified solution, making it a powerful tool for monitoring and securing IT environments. Here's a detailed overview of Wazuh:

### Key Features of Wazuh:

1. **Intrusion Detection**:
   - Monitors endpoints and network traffic to detect suspicious activities.
   - Uses rules and signatures to identify known threats and anomalies.

2. **Log Data Analysis**:
   - Collects and analyzes logs from multiple sources, including operating systems, applications, and network devices.
   - Provides detailed insights into system activities and security events.

3. **File Integrity Monitoring**:
   - Tracks changes to critical system files, directories, and configurations.
   - Alerts on unauthorized modifications, deletions, or additions.

4. **Vulnerability Detection**:
   - Scans systems for known vulnerabilities and misconfigurations.
   - Provides detailed reports to help prioritize and remediate security issues.

5. **Configuration Assessment**:
   - Ensures systems are configured according to security best practices and compliance requirements.
   - Helps maintain a secure and hardened IT environment.

6. **Security Information and Event Management (SIEM)**:
   - Correlates and aggregates data from various sources to provide a holistic view of the security landscape.
   - Enables real-time threat detection and response.

7. **Compliance Management**:
   - Supports compliance with regulatory standards such as GDPR, HIPAA, PCI DSS, and more.
   - Generates reports and maintains audit trails to demonstrate adherence to security policies.

8. **Centralized Management**:
   - Provides a centralized dashboard for monitoring and managing security across the entire IT infrastructure.
   - Facilitates easy deployment, configuration, and management of agents on endpoints.

### How Wazuh Works:

- **Agents**: Lightweight agents are installed on endpoints (servers, workstations, network devices) to collect data and monitor activities.
- **Manager**: The central server that aggregates data from all agents, applies rules, and correlates events.
- **Elastic Stack Integration**: Wazuh integrates with Elasticsearch, Logstash, and Kibana (ELK Stack) to provide powerful search, analysis, and visualization capabilities.

### Use Cases:

- **Threat Detection and Response**: Identifies and responds to security incidents in real-time.
- **Compliance Monitoring**: Ensures systems and processes comply with regulatory and internal security policies.
- **IT Operations**: Provides visibility into system performance and security, helping to optimize and secure IT operations.
- **Incident Forensics**: Analyzes historical data to investigate and understand security incidents.

### Conclusion:

Wazuh is a versatile and robust security platform suitable for organizations of all sizes. Its open-source nature, combined with comprehensive features, makes it an excellent choice for enhancing security posture, ensuring compliance, and effectively managing security incidents.

In case you need it (most likelyyou do)
A step-by-step tutorial on how to set up Wazuh on a Linux server to monitor both a Linux and a Windows machine.

### Prerequisites
- A Linux server for Wazuh Manager
- A client Linux machine
- A client Windows machine

### Step 1: Install Wazuh Manager on the Linux Server
1. **Update the package lists:**
   ```bash
   sudo apt-get update
   ```

2. **Install necessary packages:**
   ```bash
   sudo apt-get install curl apt-transport-https lsb-release gnupg2
   ```

3. **Add Wazuh repository and key:**
   ```bash
   curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | sudo apt-key add -
   echo "deb https://packages.wazuh.com/4.x/apt stable main" | sudo tee /etc/apt/sources.list.d/wazuh.list
   ```

4. **Install Wazuh Manager:**
   ```bash
   sudo apt-get update
   sudo apt-get install wazuh-manager
   ```

5. **Start Wazuh Manager service:**
   ```bash
   sudo systemctl start wazuh-manager
   sudo systemctl enable wazuh-manager
   ```

### Step 2: Install the ELK Stack for Data Visualization
1. **Install and configure Elasticsearch:**
   ```bash
   curl -s https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
   echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-7.x.list
   sudo apt-get update
   sudo apt-get install elasticsearch
   sudo systemctl start elasticsearch
   sudo systemctl enable elasticsearch
   ```

2. **Install and configure Logstash:**
   ```bash
   sudo apt-get install logstash
   ```

   Create a Logstash configuration file:
   ```bash
   sudo nano /etc/logstash/conf.d/01-wazuh.conf
   ```

   Add the following content to the configuration file:
   ```plaintext
   input {
     beats {
       port => 5044
       codec => "json_lines"
     }
   }
   filter {
     if [agent][type] == "wazuh" {
       json {
         source => "message"
         remove_field => ["message"]
       }
     }
   }
   output {
     elasticsearch {
       hosts => ["localhost:9200"]
       manage_template => false
       index => "wazuh-alerts-4.x-%{+YYYY.MM.dd}"
     }
   }
   ```

   Start Logstash:
   ```bash
   sudo systemctl start logstash
   sudo systemctl enable logstash
   ```

3. **Install and configure Kibana:**
   ```bash
   sudo apt-get install kibana
   sudo systemctl start kibana
   sudo systemctl enable kibana
   ```

   Access Kibana at `http://<your_server_ip>:5601` and follow the on-screen instructions to set up Kibana.

### Step 3: Install and Configure Wazuh Agent on Linux Client
1. **Install Wazuh agent:**
   ```bash
   sudo apt-get install wazuh-agent
   ```

2. **Configure the agent:**
   ```bash
   sudo nano /var/ossec/etc/ossec.conf
   ```

   Modify the `<address>` tag to point to the Wazuh Manager IP:
   ```xml
   <agent_config>
     <client>
       <server>
         <address>WAZUH_MANAGER_IP</address>
         <port>1514</port>
       </server>
     </client>
   </agent_config>
   ```

3. **Register and start the agent:**
   ```bash
   sudo /var/ossec/bin/agent-auth -m WAZUH_MANAGER_IP
   sudo systemctl start wazuh-agent
   sudo systemctl enable wazuh-agent
   ```

### Step 4: Install and Configure Wazuh Agent on Windows Client
1. **Download Wazuh agent for Windows from the Wazuh website.**

2. **Run the installer and follow the installation prompts.**

3. **Configure the agent:**
   - During installation, you will be prompted to enter the Wazuh Manager IP address and the agent name.

4. **Register the agent:**
   - Use the Wazuh Manager to add the Windows agent manually if not auto-registered.

### Step 5: Verify and Monitor
1. **Access Wazuh dashboard in Kibana:**
   - Navigate to the Discover tab and select the `wazuh-alerts-*` index pattern.
   - You should see logs and alerts from both the Linux and Windows agents.

2. **Check agent status:**
   - On the Wazuh Manager, you can check the status of connected agents using:
     ```bash
     sudo /var/ossec/bin/list_agents -c
     ```

### Step 6: (Optional) Enable SSL for Secure Communication
1. **Generate SSL certificates for the manager and agents.**
2. **Configure Wazuh Manager and agents to use SSL.**
   - Modify the `ossec.conf` file on both manager and agents to include SSL settings.

By following these steps, you should have a fully functional Wazuh setup on a Linux server monitoring both Linux and Windows machines, with a Kibana interface for visualization and analysis of security events.

Through this project, the organization achieved a robust and scalable security infrastructure, capable of identifying and mitigating threats efficiently, thereby significantly improving its overall security posture.
