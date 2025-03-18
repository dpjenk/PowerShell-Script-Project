POWERSHELL SCRIPT PROJECT

Objective:

The PowerShell Script project is designed to dissect and analyze a potentially malicious Base64 script to reveal any security risks. This hands-on experience was designed to deepen understanding of network security, PowerShell attack patterns, and defensive strategies.

Skills Learned:

- Proficiency in analyzing and interpreting PowerShell scripts.
- Utilizing CyberChef in order to decode Base64 encoding
- Development of critical thinking and problem-solving skills in cybersecurity.

Tools Used: 

- CyberChef (a free, open-source, web-based application designed for performing data manipulation and analysis tasks within a web browser and offering a wide range of operations for encoding, decoding, encryption, and more.)

Steps:

1) After opening the script.txt file in Notepad I can see that this is a powershell.exe file with several parameters.

Figure 1:

<img width="630" alt="PS1" src="https://github.com/user-attachments/assets/97ea395e-a57c-47b6-af1c-57a2d7a86bbd" />

 
A quick Google search allowed me to decipher the pertinent parameters:

-Enc is shorthand for -EncodedCommand which allows PowerShell to accept a Base64 encoded command. Apparently, this is used to obfuscate the script making it more difficult to detect and analyze its contents.

-W is shorthand for -WindowStyle and the Hidden value makes the session invisible to the user when the script is executed.

-NonI is shorthand for -Noninteractive meaning the session will not require user input during script execution.

2) In order to decode this Base 64 script, I used the CyberChef online tool.

3) After decoding from Base64 I noticed numerous NULL bytes. I then applied the “Remove Null Bytes” filter to make the content readable.

Figure 2:

<img width="637" alt="PS2" src="https://github.com/user-attachments/assets/34cceb33-874b-43f1-b066-e9a82c0895fb" />


Figure 3:

<img width="638" alt="PS3" src="https://github.com/user-attachments/assets/7a408d9f-84fe-413b-9a9e-b41b53a95760" />


4) System.Net uses the class “WebClient” to download or upload data to the internet. In this case, files can be downloaded from a URL.

5) This code is used to set the proxy credentials for authentication in the PowerShell script: “Proxy.Credentials =  System.Net.CredentialCache.DefaultNetworkCredentials”
6) 
According to my online research, PowerShell does not use the system’s specified proxy server by default when connecting to external web resources, so they must be specified.

The definition of “DefaultNetworkCredentials” according to Microsoft Learn is “the authentication credentials for the current security context in which the application is running. For a client-side application, these are usually the Windows credentials (username, password, and domain) of the user running the application.”

It seems that the command is simply using the current security context (username, password, and domain) to set the proxy authentication in the script to make the web request to ensure that it is successful.

8) The “$DownloadString” is pointing to the URL:
"http://98[.]103[.]103[.]170[:]7443/index[.]asp" in order to download the malicious payload. 


