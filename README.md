# HP ProLiant DL360 G7 iLO 3 Setup Log & Instructions

## 1. Connect iLO Port
- Connect the iLO port of the server to a network switch or router.

## 2. Find the Server IP Address
- If you have access to the router or switch, check the DHCP client list for the server's IP address.
- If you do not have access, use Nmap (Zenmap) to scan your local network:
  - **Target:** `192.168.x.1/24` (replace `x` with your network's default, usually `1` or `0`)
  - **Profile:** Intense scan
  - **Command:**  
    ```
    nmap -T4 -A -v 192.168.1.0/24
    ```
  - Example: In my case, the server's IP is `192.168.1.33`.

## 3. Configure Windows 10 for iLO Access
- Open **Internet Options**.
- Go to the **Advanced** tab and scroll down.
- Enable the following options:
  - Use TLS 1.0, 1.1, 1.2, 1.3
  - Use SSL 3.0

## 4. Configure Microsoft Edge for IE Mode
- Open **Microsoft Edge**.
- Go to **Settings** > **Default browser**.
- Set **Allow sites to be reloaded in Internet Explorer mode (IE mode)** to **Allow**.
- Click **Add page** and enter your server's IP address, e.g. `https://192.168.1.33/`.

## 5. Access iLO Login Page
- Navigate to the added page in Edge.
- You should see the iLO login page.

## 6. Log In
- Log in using the default username and password for your server.

Go to **Administration** → **Licensing**.  
Apply your iLO license to enable the Remote Console feature.  
Once licensed, go to **Remote Console** and launch it.

## Managing HDDs and Configuring RAID (During Boot)

1. **Power on or reboot the server.**
2. **Watch for the message:**  
   *Press any key to view Option ROM messages*  
   - Quickly press any key (the spacebar works well).

3. **Enter RAID/ORCA Utility:**  
   - When prompted, press **F8** to launch the RAID setup utility (Option ROM Configuration for Arrays, ORCA).

4. **Check RAID Volumes:**  
   - In ORCA, verify if your RAID volume is listed and check its status.

5. **Create a Logical Drive (if needed):**  
   - If no logical drive exists or it’s disabled:
     - Select **Create Logical Drive**.
     - Choose your desired RAID level (e.g., RAID 1, RAID 5).

6. **Configure RAID 5 (Recommended):**
   - Select **RAID 5** (recommended for 4 drives).
   - **Set Parity Group Count:**  
     - Enter **4** (since you have 4 drives).
   - **Spare Drive Option:**  
     - Leave **Use one drive as spare** unchecked unless you want a hot spare (note: enabling this reduces usable space).
   - **Boot Partition Option:**  
     - Select **Disable (4GB maximum)** unless you require a larger boot partition (most installations work with this setting).

7. **Create the Logical Drive:**  
   - Press **Enter** to create and initialize the RAID 5 array.

8. **Save and Exit:**  
   - Save your configuration and exit ORCA.

9. **Reboot the Server:**  
   - Allow the server to reboot.

10. **Logical Drive Status Prompt:**  
    - If prompted about logical drive status at the next boot (e.g., if the drive is disabled), press **F2** to re-enable it.

## Installing an Operating System via iLO 3 Remote Console (Using an ISO Image)

1. **Ensure iLO Remote Console is Licensed and Enabled**
   - Complete the licensing steps above to enable the Remote Console feature.

2. **Access the iLO Web Interface**
   - Open Microsoft Edge (in IE mode, as described above).
   - Navigate to your server’s iLO IP address and log in.

3. **Launch the Remote Console**
   - Go to **Remote Console** in the iLO web interface.
   - Click **Launch** to open the Remote Console window (Java or .NET client may be required; follow prompts to install if needed).

4. **Mount the OS ISO Image**
   - In the Remote Console window, look for the **Virtual Media** or **Virtual Drives** menu.
   - Select **Virtual Media** > **Image CD/DVD-ROM** (or similar option).
   - Click **Browse** and select your OS ISO file from your local computer.
   - Click **Connect** or **Mount** to attach the ISO as a virtual CD/DVD drive to the server.

5. **Reboot the Server and Boot from the ISO**
   - In the Remote Console, reboot the server if it is not already powered off.
   - During POST, press the appropriate key (usually **F11** or **F12**) to access the **Boot Menu**.
   - Select the virtual CD/DVD drive (the mounted ISO) as the boot device.

6. **Install the Operating System**
   - Follow the on-screen instructions to install your operating system as you would from a physical CD/DVD.

---

**Notes:**
- Replace IP addresses and network details with those specific to your environment.
- Adjust the number of drives and RAID level as needed for your setup.
- Creating a hot spare is optional but provides automatic rebuild protection.
- Replace any example values with those specific to your environment.

**Tips:**
- If the server does not boot from the virtual media, check the boot order in the BIOS/UEFI settings.
- After installation, remember to disconnect the ISO from Virtual Media to avoid booting from it again.