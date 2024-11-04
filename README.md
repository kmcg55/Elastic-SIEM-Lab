# Elastic-SIEM-Lab
Setting up a home lab with Elastic Cloud web portal and a Kali VM via VirtualBox. This is a walkthrough based on [Abdullah Ali's blog post](https://medium.com/@aali23/a-simple-elastic-siem-lab-6765159ee2b2). 

## Initial setup
Download and install Oracle's [Virtual Box Software](https://www.virtualbox.org/wiki/Downloads). Then download a pre-built Kali virtual machine (VM) from the [Kali official website](https://www.kali.org/get-kali/#kali-virtual-machines). Set up an account with Elastic and begin an [Elastic Cloud free trial](https://cloud.elastic.co/registration) to gain access to the [web portal](https://cloud.elastic.co). Next, boot up the Kali VM and install the Elastic Defend Agent with the given `tar` command in the terminal. Confirm the agent is installed by running `sudo systemctl status elastic-agent.service` 

![Booting up the Kali VM](https://github.com/kmcg55/Elastic-SIEM-Lab/blob/master/img/image1.jpg)

![Elastic agent installation confirmation](https://github.com/kmcg55/Elastic-SIEM-Lab/blob/master/img/image2.jpg)

Now our logs are ready to be collected and forwarded in the Elastic Cloud Console.

## Generating security events
Run a few exploratory `nmap` scans of your host machine to confirm the Elastic agent is forwarding and collecting logs properly.

![Initial nmap scans](https://github.com/kmcg55/Elastic-SIEM-Lab/blob/master/img/image3.jpg)

(To get your host machine's IP address, run `ifconfig -a` on Linux/macOS or `ipconfig /all` on Windows.)

Confirm these events were logged by searching in the Observability > Logs tab of the Elastic Deployment. 

## Creating a dashboard to visualize events
Create a simple visualization of events in the Dashboard app under the Analytics section.

![Test dashboard](https://github.com/kmcg55/Elastic-SIEM-Lab/blob/master/img/image4.jpg)

## Creating an alert for nmap scans
Create a new security alerts that detects nmap scans within the event logs. After defining and configuring the rule, set an action that will be taken once the alert is triggered. For example, you can send an email with a report of the rule execution: 
![Setting an email alert for the rule](https://github.com/kmcg55/Elastic-SIEM-Lab/blob/master/img/image5.jpg)

Now, any nmap scans will trigger an alert and a report will be sent to my Gmail address. This alert is very simple and more customized and complex rules can be configured to your liking, depending on the security posture of your home network/organization.
