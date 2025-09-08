## What You Need for this Project

-   A computer with a Web browser.

## Purpose

To practice threat hunting, using the [**Boss of the SOC (BOTS) Dataset**](https://github.com/splunk/botsv1).

## Connecting to My Splunk Server

Go here: **[https://splunk.samsclass.info](https://splunk.samsclass.info/)** or here: **[https://splunk2.samsclass.info](https://splunk2.samsclass.info/)**

Log in as  **student1**  with a password of  **student1**

The Splunk main page opens, as shown below.

![](https://samsclass.info/50/proj/p1xbots2.png)

At the top left, click "**Search & Reporting**".

The "Search" page opens, as shown below.

![](https://samsclass.info/50/proj/p1xbots3.png)

----------

# Introduction to Splunk & the BOTS Data

## Sampling the Data

In the Search box, type

> **`index="botsv1"`**

On the right side, click the "**Last 24 hours**" box and click "**All time**", outlined in red in the image below.

![](https://samsclass.info/50/proj/botsv1-1.png)

On the left side, under the Search box, click "**No Event Sampling**" and click "**1: 100**"

On the right side, click the green magnifying-glass icon

The search finishes within a few seconds, and finds approximately 9,452 results, as shown below. (The number varies because the sampling is random.)

There are actually 100x as many events, but we are only looking at 1% of them for now.

![](https://samsclass.info/50/proj/p1xbots4.png)

## Viewing Sourcetypes

On the lower left, in the "SELECTED FIELDS" list, click the blue **sourcetype** link.

A "sourcetype" box pops up, showing the "Top 10 Values" of this field, as shown below.

Notice these items:



_Note: because the sampling is random, you may see different items near the bottom of this list._

![](https://samsclass.info/50/proj/p1xbots5.png)
|Sourcetype| Sensor |
|--|--|
|**XmlWinEventLog:Microsoft-Windows-Sysmon/Operational** | _"Sysmon", a Windows monitoring tool from Microsoft_ |
|**stream:smb**,**stream:ip**,**stream:tcp**,**stream:http**  | _"Splunk Stream", which monitors live network traffic_ |
| **suricata** | _The Suricata Intrusion Detection System (IDS)_ |
|**wineventlog** and **WinRegistry**  | _Windows OS_ |
| **fgt_traffic** and **fgt_utm** | _Fortigate firewalls_ |








## Viewing stream:http Events

In the "sourcetype" box, in the "Top 10 Values" list, near the bottom, if it is visible, click **stream:http**

Splunk adds

> **`sourcetype="stream:http"`**

to the search and finds approximately 252 results, as shown below.

If there is no  **stream:http**  item in the list, just type it into the query.

![](https://samsclass.info/50/proj/p1xbots6.png)

Scroll down to examine the most recent event. Splunk has parsed this event into many fields, shown in red, including  **c_ip**, the client IP address, as shown below.

These fields are explained  [here](https://docs.splunk.com/Documentation/StreamApp/7.1.2/DeployStreamApp/FileTransfer#HTTP).

![](https://samsclass.info/50/proj/p1xbots7.png)

## Viewing HTTP Events for imreallynotbatman.com

In the Search box, at the right end, add this text:

> **`imreallynotbatman.com`**

251 events are found, as shown below. (The sampling is random, so you may not see the exact events shown below.)

![](https://samsclass.info/50/proj/p1xbots8.png)

Scroll through the first few events found, and note these items, highlighted in the image below.

-   You may see obvious attack URLs, such as the directory traversal path containing  **../../../../**  shown below.
-   Many header fields reference a  **Web Vulnerability Scanner**

![](https://samsclass.info/50/proj/p1xbots9.png)

## Take Notes

Tip: take notes of the flags you find as you go.

Several flags require you to use information from a previous challenge.

----------

# Level 1: Finding Attack Servers (20 pts + 15 extra)

## BOTSv1 1.1: Scanner Name (5 pts)

Find the brand name of the vulnerability scanner, covered by a green box in the image above.

## BOTSv1 1.2: Attacker IP (5 pts)

Find the attacker's IP address.

## BOTSv1 1.3: Web Server IP (5 pts)

Find the IP address of the web server serving "imreallynotbatman.com".

## BOTSv1 1.4: Defacement Filename (10 pts)

Find the name of the file used to deface the web server serving "imreallynotbatman.com".

Hints:

-   It was downloaded by the Web server, so the server's IP is a client address, not a destination address.
-   Remove the filter to see all 9 such events. Examine the  **uri**  values.
-   immediately notice that the same user was logging in twice from different physical locations that's what you need

-  We're going to find traffic that went backwards through the network now a proper network is designed so servers can only be servers you should not be able to open a browser on the web server and go to the web and download something there's two reasons for that the first reason is you might download a malicious thing and may affect the server with malware if you need to put a file on the server you should download it on a workstation scan it for Vi and then move it over with a file share or something the second reason and more important is if you watched Caitlyn's hacking demonstration in 123 today you've seen this attackers typically use a reverse shell the first thing they do when they get the ability to run code on your system is run code that will call out to the command and control server and put you under remote control so they will try to initiate an outgoing connection from your server and you should not allow that your firewalls should be configured to prevent that you should only allow incoming requests to the web server never outcoming requests from the web server so here's a question did the web server make any outgoing HTTP requests now right here I've got a list of all the HTTP requests but I can filter them by Source IP so if I go down here and look here's say um Source IP well all these are coming from one of these two sources

## BOTSv1 1.5: Domain Name (10 pts)

Find the fully qualified domain name (FQDN) used by the staging server hosting the defacement file.

Hints:

-   Examine the 9 events from the previous challenge. Look at the  **url**  values.

> # Splunk References
> 
> **[Search CheatSheet](https://wiki.splunk.com/images/2/2b/Cheatsheet.pdf)**
> 
> **[Search command CheatSheet](https://wiki.splunk.com/images/a/a3/Splunk_4.x_cheatsheet.pdf)**

----------

# Level 2: Identifying Threat Actors (20 pts + 30 extra)

## BOTSv1 2.1: Staging Server IP (10 pts)

In Level 1, you found the staging server domain name (used to host the defacement file). Find that server's IP adddress.

Hints:

-   Search for HTTP GET events containing the target FQDN.

## BOTSv1 2.2: Leetspeak Domain (10 pts)

Use a search engine (outside Splunk) to find other domains on the staging server. Search for that IP address. Find a domain with an name in Leetspeak (like "1337sp33k.com").

[**Alienvault**](https://otx.alienvault.com/indicator/ip/23.22.63.114)  is useful.

## BOTSv1 2.3: Brute Force Attack (15 pts)

Find the IP address performing a brute force attack against "imreallynotbatman.com".

Hints:

-   Find the 15,570 HTTP events using the POST method.
-   Exclude the events from the vulnerability scanner.
-   Examine the  **form_data**  of the remaining 441 events.
-   To make a useful table, add this to your query:
    
    > **`| table _time, form_data`**
    

## BOTSv1 2.4: Uploaded Executable File Name (15 pts)

Find the name of the executable file the attacker uploaded to the server.

Hints:

-   Find the 15,570 HTTP events using the POST method.
-   Exclude the events from the vulnerability scanner.
-   Search for common Windows executable filename extensions.

----------

# Level 3: Using Sysmon and Stream (20 pts + 30 extra)

## BOTSv1 3.1: MD5 (10 pts)

In Level 2, you found the name of an executable file the attackers uploaded to the server.

Find that file's MD5 hash.

Hints:

-   Read about  **[Sysmon Event IDs](https://docs.microsoft.com/en-us/sysinternals/downloads/sysmon)**
-   Find events from Sysmon for process creation.
-   Examine  **cmdline**  to find the correct event.

## BOTSv1 3.2: Brute Force (10 pts)

What was the first brute force password used?

Hints:

-   Start with 1:10 sampling.
-   Find events containing "login".
-   Find top values of "url".
-   Examine the "form_data" values to identify the brute force attack.

## BOTSv1 3.3: Correct Password (10 pts)

What was the correct password found in the brute force attack?

Hints:

-   Find the events with the "form_data" values indicating a login attempt.
-   There are two different "http_user_agent" values.

## BOTSv1 3.4: Time Interval (10 pts)

How many seconds elapsed between the time the brute force password scan identified the correct password and the compromised login? Round to 2 decimal places.

Hints:

-   HINT: Find the two events with the correct password in the "form_data" field.

## BOTSv1 3.5: Number of Passwords (10 pts)

How many unique passwords were attempted in the brute force attack?

Hints:

-   Examine  **http_user_agent**  values.

----------

# Level 4: Analyzing a Ransomware Attack (20 pts + 160 extra)

## BOTSv1 4.1: IP Address (5 pts)

What was the most likely IP address of we8105desk on 24AUG2016?

Hints:

-   Search for  **we8105desk**  -- you find 181,012 events.
-   Examine the  **source**  field -- there are 10 values.
-   Explore  **stream**  sources with protocols used in  [**Active Directory logins**](https://www.networkworld.com/article/2231877/ad-logons-and-network-traffic.html).
-   Find events on that day and look at their IP addresses.

## BOTSv1 4.2: Signature ID (5 pts)

Amongst the Suricata signatures that detected the Cerber malware, which one alerted the fewest number of times? Submit ONLY the signature ID value as the answer. (No punctuation, just 7 integers.)

Hints:

-   Search for  **Cerber**  -- you find 21,596 events.
-   Examine the  **source**  field -- there are 4 values.
-   Explore the source type associated with Suricata.

## BOTSv1 4.3: FQDN (15 pts)

What fully qualified domain name (FQDN) does the Cerber ransomware attempt to direct the user to at the end of its encryption phase?

Hints:

New process: Aug 2, 2021:

-   Find events with a sourcetype of  **suricata**
-   Restrict the search to events with "alert signature" containing "Onion domain lookup"
-   Restrict the time to within one second of those events
-   Look in the "stream:dns" events, in the "query" field

Old process:

-   Examine the five Suricata alerts about  **Cerber**. View them as "raw text" in time order.
-   Find a time delay and the domain lookup events after it. Note the latest time of those events.
-   Use the "Date time range" option of Search to narrow the time range to just a few seconds before the Suricata alert. Check to make sure you can still find the Suricata alerts. You may have to adjust the time by am hour or two to compensate for time zone differences.
-   Search all events in that small time range. Examine Suricata events. Look at  **dns**-related fields.

## BOTSv1 4.4: Suspicious Domain (15 pts)

What was the first suspicious domain visited by we8105desk on 24AUG2016?

Hints:

-   Find the Suricata events on that day. There are 86,579 of them.
-   Examine the  **src_ip**  field. Restrict your query to the desired value.
-   Examine the  **event_type**  field. Restrict your query to events that load Web pages. There are 38 of them.
-   Examine the hostnames visited. There are ten of them. Investigate them with Google and find the one that's known to be malicious.

## BOTSv1 4.5: VB Script (15 pts)

During the initial Cerber infection a VB script is run. The entire script from this execution, pre-pended by the name of the launching .exe, can be found in a field in Splunk. What is name of the first function defined in the VB script?

Hints:

-   Search for events with both a filename extension for VB script and an  **.exe**  extension. There are 16 of them.
-   Examine the  **body**  field. Find the malicious one.

## BOTSv1 4.6: Field Length (15 pts)

During the initial Cerber infection a VB script is run. The entire script from this execution, pre-pended by the name of the launching .exe, can be found in a field in Splunk. What is the length in characters of the value of this field?

Hint:

-   Find the length of the Splunk field, not the length of the script itself.  [This](https://community.splunk.com/t5/Splunk-Search/length-of-string-Urgent-Requirment-pls/m-p/303177)  may be helpful.
-   There are three events with fields that match this description. Use the longest length of those three fields. The longer ones contain the same script, but ampersands are HTML-encoded which makes the field longer.

## BOTSv1 4.7: USB key (15 pts)

What is the name of the USB key inserted by Bob Smith?

Hints:

-   Find events with SourceType of WinRegistry
-   Search for "FriendlyName", as shown  [here](https://docs.microsoft.com/en-us/windows-hardware/drivers/usbcon/usb-device-specific-registry-settings).

## BOTSv1 4.8: Server Name (5 pts)

Bob Smith's workstation (we8105desk) was connected to a file server during the ransomware outbreak. What is the domain name of the file server?

Hints:

-   Examine SMB stream data for Bob's workstation during the outbreak
-   Find events with a "path" by adding path="*" to the query
-   The server name resembles Bob's workstation name.

## BOTSv1 4.9: IP Address (15 pts)

Bob Smith's workstation (we8105desk) was connected to a file server during the ransomware outbreak. What is the IP address of the file server?

Hints:

-   Search for the server's name. Examine the  **source**  of those events. Look for source types that record raw network data and would therefore include IP addresses.

## BOTSv1 4.10: PDFs (20 pts)

How many distinct PDFs did the ransomware encrypt on the remote file server?

Hints:

-   Search for  **.pdf**
-   Restrict your search for the "unknown"  **app**
-   Find all unique filenames. Remove filenames outside the time range of the attack.

## BOTSv1 4.11: Process ID (15 pts)

The VBscript found above launches 121214.tmp. What is the ParentProcessId of this initial launch?

Hints:

-   Search for  **121214.tmp**  -- you find 190 events.
-   Examine the  **EventDescription**  field and focus on the one most closely related to the question.
-   Examine the  **CommandLine**  field.

## BOTSv1 4.12: Text Files (15 pts)

The Cerber ransomware encrypts files located in Bob Smith's Windows profile. How many .txt files does it encrypt?

Hints:

-   Find all events including**.txt**  and find the path to Bob's Windows profile.
-   Add Bob's Windows profile path to the search. To search for a backslash, enter two backslashes.
-   Examine the file paths and remove the ones outside Bob's profile.

## BOTSv1 4.13: File Name (15 pts)

The malware downloads a file that contains the Cerber ransomware cryptor code. What is the name of that file?

Hints:

-   Search for HTTP downloads from the suspicious domain you found in flag BOTSv1 4.4 above.
-   The filename has a surprising extension. Research that filename outside Splunk to verify that it's related to Cerber.

## BOTSv1 4.14: Obfuscation (10 pts)

Now that you know the name of the ransomware's encryptor file, what obfuscation technique does it likely use?

Hints:

-   Research the file using online resources, outside Splunk, to find this.
