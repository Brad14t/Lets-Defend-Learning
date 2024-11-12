# Lets-Defend-Learning

**WireShark query documentation:** https://www.wireshark.org/docs/man-pages/wireshark-filter.html


# Lets Defend SOC Fundamentals: 

Main Takeaways:

# PCAP Analysis using WireShark

First step is to open provided PCAP file.

<img width="951" alt="Screenshot 2024-11-11 142748" src="https://github.com/user-attachments/assets/7c16feb8-cd8d-4eb6-a7a9-4b7244df8571">

**Q1 - In network communication, what are the IP addresses of the sender and receiver?**

For me I couldnt find anything sticking out to me at a quick glance. Im using the provided hint:

<img width="452" alt="Screenshot 2024-11-11 143222" src="https://github.com/user-attachments/assets/4119f270-9553-4f83-91be-1595639a2590">

I can see that the data contains "P13" to filter for this, I try to filter by frame: `frame contains "P13"`

<img width="957" alt="Screenshot 2024-11-11 143949" src="https://github.com/user-attachments/assets/87b9bf76-1fb7-49d0-b4bf-b3fd408153e8">

Now I can see a few different IP addresses. Checking to see if there is a conversation by right clicking the top packet > Follow > TCP Stream

<img width="957" alt="1" src="https://github.com/user-attachments/assets/b405665c-6152-4ea7-b54a-047f5f728570">

Now I can confirm there is a conversation between 2 parties.

<img width="637" alt="Screenshot 2024-11-11 145249" src="https://github.com/user-attachments/assets/9a5a22be-8a43-4d13-afe9-3e0222338982">

Looking back I can see the 2 IP addresses in the conversation.

<img width="405" alt="1" src="https://github.com/user-attachments/assets/b313595a-ac54-4fe3-9d4b-0366bf27e114">

**Q2 - P13 uploaded a file to the web server. What is the IP address of the server?**

To find the web server request I will be using the `http.request.method == "POST"`.

POST in short: POST is a way for the browser to send information to the server over HTTP.

<img width="955" alt="Screenshot 2024-11-11 150446" src="https://github.com/user-attachments/assets/b68a135f-f1d2-4ef4-8787-420464f19e06">

This is a good start but it isnt narrowed down enough. To narrow it down I can use the frame filter again and search for `"upload"`.

Full command: `http.request.method == "POST" and frame contains "upload"

<img width="817" alt="Screenshot 2024-11-11 150832" src="https://github.com/user-attachments/assets/28f570a4-b281-4ea3-b80b-1a0397a3338c">

Here I am given the destination IP for the question.

**Q3 - What is the name of the file that was sent through the network?**

TO find file name, select the known malicious file using the command: `http.request.method == "POST" and frame contains "upload" 

Then select the MIME drop down and locate file name.

<img width="959" alt="1" src="https://github.com/user-attachments/assets/e25fecf1-9849-4096-9e31-728c6c073548">

**Q4 - What is the name of the web server where the file was uploaded?**

To check the web server I can investigate the HTTP stream. 

Using the same query as last question right click the packet > Follow > HTP stream

<img width="781" alt="1" src="https://github.com/user-attachments/assets/885b84f9-9598-4b66-8275-bb0a4d67acba">

Next I scroll down to the information about the type of server.

<img width="584" alt="1" src="https://github.com/user-attachments/assets/01550a4e-4b7c-4b81-80d3-4e6fcc7bd855">

**Q5 - What directory was the file uploaded to?**

In the same HTTP stream as before I can see the `upload to: upload/file`

<img width="410" alt="1" src="https://github.com/user-attachments/assets/dd8b0394-bec3-4a9f-8655-e1f7be488dc5">

**Q6 - How long did it take the sender to send the encrypted file?**

To see this go back to the conversations > then filter by IP addresses and look for the conversation in Q1.

<img width="949" alt="1" src="https://github.com/user-attachments/assets/8ccbe90f-51d9-4e4e-9ecc-0da4e078f87e">












