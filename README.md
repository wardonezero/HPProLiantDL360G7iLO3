# HP ProLiant DL360 G7 iLO 3 Setup Log & Instructions

## 1. Connect iLO Port
- Connect the iLO port of the server to a network switch or router.

## 2. Find the Server IP Address
- If you have access to the router or switch, check the DHCP client list for the server's IP address.
- If you do not have access, use Nmap (or Zenmap) to scan your local network:
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

---

**Notes:**
- Replace IP addresses and network details with those specific to your environment.
- Ensure your browser and system security settings comply with your organization's policies.