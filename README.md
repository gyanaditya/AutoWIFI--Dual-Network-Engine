# AutoWifi: Dual-Network (Cellular + Wi-Fi) Routing & Tunneling for Android

> **Simultaneous Dual-Network Concurrency, Reverse Hotspot Sharing, SSH & SOCKS5 Tunneling, and Per-App VPN Split Routing.**

---

## 🌟 Introduction

In standard Android network operations, the operating system treats network interfaces as mutually exclusive: as soon as your device connects to a Wi-Fi network, Android turns off or down-prioritizes your Cellular mobile data connection. 

**AutoWifi** breaks this limitation.

Built upon Android's advanced network binding and virtualization stack (`NetworkRequest`, `WifiNetworkSpecifier`, and `VpnService`), AutoWifi allows an Android smartphone to maintain **simultaneous, concurrent connections to both Mobile Data (Cellular) and Wi-Fi networks**. Traffic can then be granularly split, forwarded, tunneled, or proxied between these two physical channels according to user-defined rules.

Whether you need to route bandwidth-heavy apps over an office Wi-Fi while keeping secure banking on 5G, tunnel traffic via dynamic SSH port forwarding, share your mobile data without toggling an Android hotspot, or automate roaming between Wi-Fi access points with the strongest BSSID, AutoWifi provides a unified control center on your phone.

---

## 🚀 Key Features

```
               ┌──────────────────────────────────────────────┐
               │         AutoWifi Multi-Path Engine           │
               └──────┬────────────────────────────────┬──────┘
                      │                                │
         ┌────────────▼────────────┐      ┌────────────▼────────────┐
         │     Cellular (4G/5G)    │      │    Wi-Fi (WPA2/Open)    │
         └────────────┬────────────┘      └────────────┬────────────┘
                      │                                │
          Default App Traffic             Tunnel Layer (SSH/SOCKS/VPN)
          Background Sync                 High-Bandwidth Media
          Cellular-Bound Apps             Per-App Split Allowed List
```

### 1. Simultaneous Dual-Network Concurrency
- Keeps your primary cellular connection online while binding Wi-Fi as a dedicated second network layer.
- Supports both secured Wi-Fi networks (WPA2/WPA3 PSK) and open / password-free networks with automatic capability detection.
- Includes automated BSSID roaming that dynamically monitors signal quality and roams to the strongest access point seamlessly.

### 2. VPN Mode with Full Per-App Split Tunneling
- **Route All Apps**: Complete system-wide VPN encryption and routing through the Wi-Fi tunnel.
- **App-Split Mode**: Select exactly which applications, system services, or add-ons use Wi-Fi, while all other applications route through high-speed Cellular data.
- Full package visibility support: lists user-installed applications, pre-installed system apps, background frameworks, and add-ons.

### 3. All-in-One SOCKS5 Proxy Server
- Runs an embedded, multi-threaded SOCKS5 server directly on the device with configurable listening ports (default: `9999`).
- **Wi-Fi Route**: Directs all SOCKS proxy traffic out through the Wi-Fi interface.
- **Cellular Route ("Reverse Hotspot Magic")**: Routes outbound SOCKS traffic over Cellular while listening on the Wi-Fi LAN. Other devices connected to your Wi-Fi or hotspot can share your mobile data through `tun2socks` without requiring you to enable Android's native hotspot!

### 4. SSH Tunneling & Port Forwarding
- Embedded Apache SSHD client supporting SSH key & password authentication.
- **Dynamic Port Forwarding**: Turns the local phone into an encrypted SOCKS gateway.
- **Remote Port Forwarding**: Exposes internal device sockets or local services to remote servers.
- **Standalone Port Forwarding**: Run forwarding rules independently without enabling full proxy modes.

### 5. Multi-Profile Management & Biometric Protection
- Save unlimited distinct network configurations (Home, Office, Lab, Field).
- One-tap profile activation with live status monitors.
- Biometric authentication (fingerprint/face unlock) protects saved passwords and credentials from unauthorized exposure.
- Local JSON backup and restore with integrity validation.

### 6. Built-in Network Diagnostic Utilities
- **Ping Utility**: ICMP and socket-based latency measurements.
- **Subnet Scanner**: Discover active IP addresses across your connected subnet.
- **Port Scanner**: Check open TCP services across local or remote hosts.
- **Bonjour / mDNS Discovery**: Discover zero-config LAN services (`_http._tcp`, `_ssh._tcp`, etc.) with FIFO resolve queue management.

---

## 🪄 Feature Spotlight: The "Reverse Hotspot" Magic

Have you ever had a friend ask for your hotspot, but you didn't want to disconnect from your current Wi-Fi or drain your battery running an Android mobile hotspot?

With AutoWifi's **Cellular SOCKS Routing**, you can share your cellular connection in reverse:

```
┌─────────────────┐        Wi-Fi / Hotspot        ┌─────────────────┐
│     Friend      │ ◄───────────────────────────► │  Your Device    │
│  (Hotspot ON)   │       Local LAN (9999)        │   (AutoWifi)    │
└────────┬────────┘                               └────────┬────────┘
         │                                                 │
         │ Uses tun2socks (Target: AutoWifi IP:9999)      │ Routes out via 4G/5G
         ▼                                                 ▼
   Internet Access                                   Mobile Data Carrier
```

1. Tell your friend to turn on **their** hotspot and install [tun2socks](https://play.google.com/store/apps/details?id=com.github.xfalcon.v2ray) from the Play Store.
2. Connect AutoWifi to their hotspot SSID.
3. In AutoWifi **Settings**, select **Cellular Route** under SOCKS Routing.
4. Tap **Start** in SOCKS mode.
5. In your friend's `tun2socks` app, enter your device's AutoWifi Wi-Fi IP and port `9999`.
6. Your friend now browses the web through **your** cellular internet, with zero battery strain from hosting a hotspot on your phone!

---

## 📱 Tech Specs

- **Target SDK**: Android 16 / 15 (`API 36`)
- **Minimum SDK**: Android 10 (`API 29`)
- **Language**: Java 11
- **Architecture**: Single-Task Activity with Foreground Service Daemon
- **Build System**: Gradle 8.13 with Kotlin DSL (`build.gradle.kts`)

---

## 👨‍💻 Developer & Contact

**Developed by**: Dr. Gyanaditya Mourya  
**Contact / Feedback**: [dr.gyanaditya@gmail.com](mailto:dr.gyanaditya@gmail.com)  
**Package Name**: `com.gyan.autowifi`

