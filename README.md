# Lets-Defend-Learning

**WireShark query documentation:** https://www.wireshark.org/docs/man-pages/wireshark-filter.html


# Lets Defend SOC Fundamentals: 

Main Takeaways:

# PCAP Analysis using WireShark

First step is to open provided PCAP file.

<img width="951" alt="Screenshot 2024-11-11 142748" src="https://github.com/user-attachments/assets/7c16feb8-cd8d-4eb6-a7a9-4b7244df8571">

**1-** In network communication, what are the IP addresses of the sender and receiver?

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

**2-** P13 uploaded a file to the web server. What is the IP address of the server?

To find the web server request I will be using the `http.request.method == "POST"`.

POST in short: POST is a way for the browser to send information to the server over HTTP.

<img width="955" alt="Screenshot 2024-11-11 150446" src="https://github.com/user-attachments/assets/b68a135f-f1d2-4ef4-8787-420464f19e06">

This is a good start but it isnt narrowed down enough. To narrow it down I can use the frame filter again and search for `"upload"`.

Full command: `http.request.method == "POST" and frame contains "upload"

<img width="817" alt="Screenshot 2024-11-11 150832" src="https://github.com/user-attachments/assets/28f570a4-b281-4ea3-b80b-1a0397a3338c">

Here I am given the destination IP for the question.








