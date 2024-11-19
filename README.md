# Lets Defend SOC167 - LS Command Detected in Requested URL


**Summary:**

The alert flagged a potential malicious Linux payload due to the keyword "ls" in the URL. The source IP belongs to the device ElliotPRD within the network, which had been accessing letsdefend.io via Cloudflare. While ElliotPRD's browsing history and connections match the alert, the destination IP is verified as safe by VirusTotal and Cisco Talos Intelligence. This was a false positive, as the "ls" keyword was mistakenly identified as a possible Linux command injection attempt.

**Incident Response:**

Start by selecting the `>>` to create a new case.

Then Start Playbook.

<img width="569" alt="Screenshot 2024-11-19 110144" src="https://github.com/user-attachments/assets/622d529b-38c3-4d80-be74-692962b8085a">

Now inside the playbook, I want to start collecting information about the incident.

I start by looking at the provided data.

<img width="700" alt="Screenshot 2024-11-19 110535" src="https://github.com/user-attachments/assets/5e4fdff8-15fb-434d-b3f8-e0c9b486ef13">

Looking at the information I can see the alert was triggered due to "URL Contains LS". 

URL containing LS meaning ls the command.

The Requested URL: https://letsdefend.io/blog/?s=skills

Next is to search for the traffic from the source IP. I filter the logs to only show data associated with the source IP of 172.16.17.46.

<img width="657" alt="Screenshot 2024-11-19 111206" src="https://github.com/user-attachments/assets/3d6f80dd-4ca6-448a-8c55-c2e07c560bb5">

This didnt show much of anything. 

Next I check the EDR, and filter for destination and source port to see if any our in "My network".

Looking up the Destination IP: 188.114.96.15 OR Source IP: 172.16.17.46, EliotPRD Pops up.

<img width="296" alt="Screenshot 2024-11-19 131850" src="https://github.com/user-attachments/assets/337c9fa1-cb06-41a7-9ad6-3fc392ad13e9">

Scrolling down in the browser history I can see the matching command.

<img width="614" alt="1" src="https://github.com/user-attachments/assets/4354edd1-9072-4cad-bdbf-ad00be3264fb">

The reason that endpoint is showing up for the destination IP is because in the `Network History` tab you can see the connections between the 2 IP's.

<img width="539" alt="Screenshot 2024-11-19 132311" src="https://github.com/user-attachments/assets/cf804e94-9b3f-418f-b5ce-b5f6065b6cc2">

Looking through the endpoint nothing seems suspicous yet. The user was just looking into the Lets Defend website.

I'll continue to answer the questions in the playbook with my knowlege gained from the investigation.

<img width="513" alt="Screenshot 2024-11-19 132858" src="https://github.com/user-attachments/assets/7ffedb21-1a06-417a-806d-4805890f3c19">

* Nothing in this was found to be malicous, looking through the logs and the endpoint. Everthing seems like a user was just searching the LetsDefend website.

<img width="468" alt="Screenshot 2024-11-19 133029" src="https://github.com/user-attachments/assets/1c446dd6-457d-4d76-8f9f-b75d7c5199b4">

* Looking at HTTP logs and browser history user was using LetsDefend through port 443 (HTTPS) correctly and the interaction between the source and destination remained between those 2. The redirects just brought the user back to a LetsDefend URL.
* So technicaly the answer is `Yes` since traffic was redirected.

<img width="502" alt="Screenshot 2024-11-19 133659" src="https://github.com/user-attachments/assets/73d9b67b-488e-4689-addf-f0a5681cfa23">

* Leave some breif notes of what was done. More detailed notes are within a personal collection.

<img width="435" alt="Screenshot 2024-11-19 134243" src="https://github.com/user-attachments/assets/d6a637d6-5854-4819-9d9e-d2c7afefb75c">

