# CybernightsForensics2025
Solving forensics

Historian - CyberNight 2025 Forensics CTF
Objective
In this challenge, participants are tasked with analyzing a VHDX file to uncover stored conversations. The goal is to extract the flag hidden in any chats.

Walkthrough
Step 1: Load the NBD Kernel Module
To begin, we need to load the Network Block Device (NBD) kernel module. This allows us to interact with the VHDX file as if it were a physical disk.


sudo modprobe nbd
Step 2: Connect the VHDX File to an NBD Device
Next, we connect the VHDX file to an NBD device using the qemu-nbd tool. This step makes the contents of the VHDX file accessible through the NBD interface.


sudo qemu-nbd --connect /dev/nbd0 2025-02-25T205402_historian.vhdx
Step 3: List Block Devices
We then list the block devices to confirm that the VHDX file has been successfully connected to the NBD device.


lsblk
Output:
![Screenshot 2025-03-02 043945](https://github.com/user-attachments/assets/6ab4a83f-1c82-4663-9ce3-926acfab74e6)


...
Step 4: Mount the NBD Partition
With the VHDX file connected, we mount the partition from the NBD device to access its contents.


sudo mount /dev/nbd0p1 /mnt
Step 5: Search for Chat-Related Data
Given the objective of finding stored conversations, I began searching for any directories or files related to chat applications. This led me to the AppData directory, which often contains user-specific application data.


cd /mnt/Users/FlagYard/AppData/Local/Packages/

Step 6: Discover the ChatGPT Folder
Within the Packages directory, I found a folder named OpenAI.ChatGPT-Desktop_2p2ngsdoc76g0, which indicated the presence of ChatGPT-related data.
![Screenshot 2025-03-02 044041](https://github.com/user-attachments/assets/fdcf0e83-d047-4614-9935-168cc787d826)



cd OpenAI.ChatGPT-Desktop_2p2ngsdoc76g0/

Step 7: Navigate to the IndexedDB Directory
I navigated further into the directory structure to locate the IndexedDB folder, which is commonly used by web applications to store large amounts of structured data.


cd LocalCache/Roaming/ChatGPT/IndexedDB/https_chatgpt.com_0.indexeddb.leveldb
![Screenshot 2025-03-02 044121](https://github.com/user-attachments/assets/ddea0647-8aa3-4c08-a90a-0082d2b8f5f7)


Step 8: List the Contents of the Directory
Listing the contents of the directory revealed several files, including a log file named 000003.log.


Output:
000003.log  CURRENT  LOCK  LOG  MANIFEST-000001


Step 9: Extract the Flag
Finally, I read the contents of the 000003.log file, which contained the hidden flag within the stored conversations.

![Screenshot 2025-03-02 044349](https://github.com/user-attachments/assets/fe3e3dc6-d695-449f-b2db-cd0f2b0d80e9)
![Screenshot 2025-03-02 044404](https://github.com/user-attachments/assets/6ea50a77-1767-4323-b887-e5a0b1c23a37)





