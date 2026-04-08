# OmniGuard Wi-Fi Bridge Pro (Repeater Mode)

**OmniGuard Bridge** is a powerful Android-based Wi-Fi repeater and secure gateway. It allows you to share an existing Wi-Fi connection with other devices (Laptops, PCs, Mobiles) using **Wi-Fi Direct (P2P)**. Unlike the standard Android hotspot, this app does not require cellular data and keeps your phone connected to the primary Wi-Fi while acting as a bridge.

---

## 🚀 Features

* **Wi-Fi to Wi-Fi Sharing:** Share your Wi-Fi internet without turning it off.
* **Secure Gateway:** Acts as a hardware firewall between public Wi-Fi and your personal devices.
* **Traffic Monitoring:** Real-time logging of connected devices (MAC, IP, and requested Hostnames).
* **Background Persistence:** Uses a Foreground Service with `WakeLocks` and `WifiLocks` to prevent the system from killing the connection.
* **No Root Required:** Works on standard Android devices using a high-performance HTTP/SOCKS5 proxy.

---

## 🛠️ Technical Architecture

The app functions by creating an autonomous Wi-Fi Direct Group Owner (GO). Since Android restricts native NAT routing without root, OmniGuard implements a **Local Proxy Server** to bridge the `wlan0` (Wi-Fi) and `p2p-wlan0` (Bridge) interfaces.



---

## 📥 Installation & Setup

### 1. Build the APK
1.  Clone this repository into **Android Studio**.
2.  Ensure you have the `NanoHTTPD` dependency in your `build.gradle`.
3.  Build and install the APK on your Android device.

### 2. Required Permissions
To function as a repeater, the app requires:
* `NEARBY_WIFI_DEVICES` & `ACCESS_FINE_LOCATION` (Required for Wi-Fi Direct).
* `POST_NOTIFICATIONS` (For the Foreground Service).
* **Battery Optimization:** Set to **"Unrestricted"** in Android settings to prevent disconnects.

---

## 💻 How to Connect (Windows 10/11)

Because this is a proxy-based bridge, you must manually configure your client device after connecting to the Wi-Fi Direct signal.

1.  **Connect to Wi-Fi:** Find the SSID (e.g., `DIRECT-xy-OmniBridge`) on your PC and connect using the password shown in the app.
    * *Note: If Windows asks for an 8-digit PIN, click "Connect using a security key instead" to use the password.*
2.  **Open Proxy Settings:** Search for **"Proxy Settings"** in the Windows Start menu.
3.  **Manual Proxy Setup:**
    * Toggle **"Use a proxy server"** to **ON**.
    * **Address:** `192.168.49.1`
    * **Port:** `8282`
4.  **Save:** Click Save. Your internet should now be active.



> **Pro Tip:** If websites fail to load while apps (like WhatsApp) work, disable **"Secure DNS"** in your browser settings (Chrome/Edge) to allow the proxy to handle DNS requests.

---

## 🛡️ Security & Privacy

OmniGuard is designed with security in mind:
* **Header Stripping:** Automatically removes identifying headers (`User-Agent`, `Via`, `X-Forwarded-For`) to prevent device fingerprinting on public networks.
* **DNS Protection:** Configured to route DNS queries safely through the proxy tunnel to prevent local DNS hijacking.
* **Isolation:** Connected devices sit on a private subnet, making them invisible to potential attackers on the host public Wi-Fi.

---

## 📊 Traffic Monitoring

The **Monitor** tab provides a live view of the network:
* **Device Identification:** Maps IP addresses to MAC addresses via the system `/proc/net/arp` table.
* **Request Logs:** See which domains (`google.com`, `github.com`) are being accessed by each device in real-time.

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
