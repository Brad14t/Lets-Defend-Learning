# Lets-Defend-Learning

**WireShark query documentation:** https://www.wireshark.org/docs/man-pages/wireshark-filter.html

# Badges 

<img width="120" height="100" alt="Screenshot 2024-11-12 095053" src="https://github.com/user-attachments/assets/7855fe7e-39ce-4a97-ac11-79a7f56ebd03">

<img width="120" height="100" alt="Rounded Image" src="https://github.com/user-attachments/assets/5aa58d69-238a-4ab8-81f7-ceba904b2ed8">


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

<img width="425" alt="Screenshot 2024-11-12 095053" src="https://github.com/user-attachments/assets/6f300bf2-eb8b-42e9-93f0-a06b37eddf21">

# Malicious AutoIT

**Q1 - What is the MD5 hash of the sample file?**

First is to go to file loacation. C:\Users\LetsDefend\Desktop\ChallengeFile\sample.zip 

Unzip the file and open "HashCalc" tool > select the file 

<img width="577" alt="1" src="https://github.com/user-attachments/assets/2801a4e8-b8ee-4975-beda-c86803192658">

**Q2 - According to the Detect It Easy (DIE) tool, what is the entropy of the sample file?**

First open the DIE tool > slect the "..." > select file

<img width="538" alt="1" src="https://github.com/user-attachments/assets/57cb6338-e62a-4992-9ac5-513ed4a9c7d2">

<img width="585" alt="1" src="https://github.com/user-attachments/assets/755be8d0-a699-4aa0-9e9e-dd2d3599f230">

**Q3 - According to the Detect It Easy(DIE) tool, what is the virtual address of the “.text” section?**

First go to the sections

<img width="527" alt="1" src="https://github.com/user-attachments/assets/49171808-4e26-49ef-8303-b59883b13e95">

In the sections we can see the .text virtual address.

<img width="770" alt="1" src="https://github.com/user-attachments/assets/ef697e09-425f-4013-841d-a877e9781b1e">

Required answer  format: 0x1000

**Q4 - According to the Detect Easy tool, what is the “time date stamp”?**

I can see the time stamp in the tool.

<img width="539" alt="1" src="https://github.com/user-attachments/assets/ca73fce8-84c9-4cb4-883d-d9f1287bc2e3">

**Q5 - According to the Detect It Easy (DIE) tool, what is the entry point address of the executable?**

<img width="534" alt="1" src="https://github.com/user-attachments/assets/43b7a850-035f-4d3a-bcfc-ae8a136a67b5">

Answer format: 0x42800a

**Q6 - What is the domain used by the malicious embedded code?**

First to find the domain I can use powershell to run the AutoIT- Ripper tool.

Autoit-ripper tool is a python script that can extract compiled AutoIt sample.

I open powershell and try to find the sample file.

`cd Desktop\ChallengeFile`

<img width="344" alt="1" src="https://github.com/user-attachments/assets/80124ecb-3cb3-44e8-bb18-7b1be999d867">

After some struggling to get the command to work, what worked for me is I created a new folder with the sample data.

<img width="583" alt="Screenshot 2024-11-12 113506" src="https://github.com/user-attachments/assets/dd6e09a4-9783-4a8a-8339-5a5201a1a541">

I select the Output and copy the path

**ERROR** if you are receiving a ernno 13 error code, was due to me extracting the files as a folder instead of extracting in the same directory.

Make sure to select "extract files here"

<img width="460" alt="1" src="https://github.com/user-attachments/assets/3ba12b67-79ae-4497-acbc-193bd1822328">

Now I can see it worked.

<img width="327" alt="Screenshot 2024-11-12 143749" src="https://github.com/user-attachments/assets/c4750e75-5de7-486e-8617-05db9b4198ae">

Next in the Output file I right click and open with Notepad

<img width="312" alt="1" src="https://github.com/user-attachments/assets/99945d80-1f3c-4d85-a0f1-c21efb3681f5">

Opening this I can see the script using the AutoID language.

Scrolling down I can find the domain used in the embedded code.

<img width="733" alt="1" src="https://github.com/user-attachments/assets/c673df02-9a91-4999-bdb8-f8c302d7d6ca">

**Q7 - What is the file path encoded in hexadecimal in the malicious code?**

I can find the hexadecimal on the same page.

<img width="737" alt="1" src="https://github.com/user-attachments/assets/d621b7b2-1bc0-486d-a678-74c547b53430">

After copying the hexadecimal, open Cyber Cheif in the tools to decrpty.

<img width="559" alt="1" src="https://github.com/user-attachments/assets/ee092204-d5d0-4f30-b1f4-04d843f18090">

Once inside select from Hexadecimal > then paste hexadecimal 

<img width="730" alt="1" src="https://github.com/user-attachments/assets/c51f072f-bd16-485f-9c1a-e06fecaf9c11">

**Q8 - What is the name of the DLL called by the malicious code?**

To find this scroll down to the bottom of the script.

<img width="709" alt="1" src="https://github.com/user-attachments/assets/1b30901c-019d-4e68-9175-3b11767ec3f7">







