# Lab 000 — Installing Cisco Packet Tracer and Wireshark

**Course:** CCNA Foundations → CCNP Enterprise / SD-WAN  
**Audience:** Beginners (no networking experience required)  
**Cost:** $0 for the software covered here  
**Deadline:** Complete before Lab 001  
**Platforms:** Windows, macOS, Ubuntu Linux (see compatibility notes)

## 1. Purpose

You will install **two applications**:

1. **Cisco Packet Tracer:** Build simulated networks, configure Cisco-like devices, and follow packets using its built-in **Simulation Mode**.
2. **Wireshark:** Capture and inspect **real packets from your computer's network interfaces**.

> **Important:** Wireshark does **not** capture Packet Tracer's internal simulated packets directly. Use **Packet Tracer Simulation Mode** to inspect the simulated network, and **Wireshark** to inspect your computer's real network traffic. We will use both throughout the course.

**No Cisco hardware, virtual machines, Docker, GNS3, or paid Cisco license is required for Lab 000.**

## 2. Before you begin

- Use a desktop or laptop with administrator privileges for installation.
- Have an Internet connection and a working email address.
- Allow enough disk space for the downloads and installers (at least 3 GB of available space is a practical starting point).
- **Cisco Packet Tracer:** Cisco's current published requirements list **Windows 11, macOS 12+, or Ubuntu 22.04/24.04 LTS**, an **x86-64 (amd64) processor**, **4 GB free RAM**, and **1.4 GB free storage**. Check Cisco's page for updated requirements; this list is *not* a guarantee for every machine.
- **Apple Silicon Macs (M1/M2/M3/M4/etc.):** Cisco's listed Packet Tracer requirements specify x86-64. Do **not** assume native ARM support. Check the current Cisco installer and compatibility before the course. If it does not work, contact the instructor for an approved alternative rather than installing an unofficial copy.
- **Windows 10 or other Linux distributions:** They are not listed in the above current Packet Tracer requirements; successful installation is not guaranteed. If your OS differs, tell the instructor before the deadline.
- For Wireshark, **Npcap on Windows** and **capture permissions on macOS/Linux** may require an extra setup step.

## 3. Create your free Cisco account — REQUIRED

This step **cannot be replaced by Chocolatey or Homebrew**.

1. Open: <https://www.netacad.com/courses/getting-started-cisco-packet-tracer/1000>
2. Enroll in **Getting Started with Cisco Packet Tracer** (free).
3. Create a Cisco/NetAcad account, or sign in with your existing account.
4. Confirm your email if prompted.
5. Open Cisco's official Resource Hub: <https://www.netacad.com/resources/lab-downloads>
6. Download the current **Cisco Packet Tracer** installer for your operating system.

**Do not download Packet Tracer from third-party mirror sites or unofficial package repositories.** Cisco controls distribution and authentication. You do not need to buy a Cisco course to get Packet Tracer.

## 4. Install Cisco Packet Tracer

### Windows 11

1. Download the **Windows 64-bit `.exe`** from Cisco's Resource Hub.
2. Double-click the downloaded installer and follow the wizard.
3. Accept the license terms and finish installation.
4. Launch **Cisco Packet Tracer** from the Start menu.
5. Authenticate with your Cisco/NetAcad account when prompted.

**Chocolatey users:** Do not rely on an unofficial `choco install` recipe for Packet Tracer. Cisco's official installer plus Cisco sign-in is the supported classroom path.

### macOS

1. Confirm that your processor and macOS version are compatible with the current Cisco release (see Section 2).
2. Download the **macOS `.dmg`** from Cisco's Resource Hub.
3. Open the `.dmg` and follow the installation instructions shown by the downloaded package.
4. Launch **Cisco Packet Tracer** from Applications or Launchpad.
5. Authenticate with your Cisco/NetAcad account when prompted.

**Homebrew users:** Packet Tracer is **not** part of this course's Homebrew installation workflow. Use Cisco's own download rather than an unofficial cask.

### Ubuntu 22.04 / 24.04 LTS (x86-64)

Download the **Ubuntu 64-bit `.deb`** from the Cisco Resource Hub. Open Terminal:

```bash
cd ~/Downloads
ls -1 CiscoPacketTracer*Ubuntu*64bit.deb
```

Install the downloaded file (replace the filename with the one actually displayed):

```bash
sudo apt update
sudo apt install ./CiscoPacketTracer_901_Ubuntu_64bit.deb
```

**Important:** The `901` filename is an **example corresponding to Packet Tracer 9.0.1**, not a guarantee about future release names. Use the exact file you downloaded. `apt install ./file.deb` is preferred because it also resolves available dependencies; don't start with `dpkg -i`.

Accept the license agreement if prompted, launch Packet Tracer from the application menu, and sign in to Cisco/NetAcad.

If dependencies cannot be resolved, save the terminal error text and contact the instructor. Do not start adding unrelated third-party repositories.

## 5. Install Wireshark

Use **one** of the following installation methods for your computer.

### Windows 11 — Chocolatey (recommended for students who already have it)

Open **PowerShell as Administrator**:

```powershell
choco --version
choco install wireshark -y
```

If Chocolatey is not installed, either install it from <https://chocolatey.org/install> following its official instructions **or** use the official Wireshark Windows installer at <https://www.wireshark.org/download.html>.

**Critical — Npcap:** Wireshark needs **Npcap** to capture live packets on Windows. When the installation workflow prompts you to install Npcap, **install/enable it**. If the Chocolatey installation doesn't provide Npcap or Wireshark opens without capture interfaces, run the **official Wireshark installer** and install the bundled Npcap component. Merely seeing the Wireshark GUI does **not** prove capture works.

Restart Wireshark (or Windows if requested), then launch it from the Start menu.

### macOS — Homebrew (recommended for students who already have it)

Open Terminal:

```bash
brew --version
brew install --cask wireshark-app
```

> **Important package-name change:** Current Homebrew catalogs list the GUI application as **`wireshark-app`** (formerly `wireshark`). Prefer `wireshark-app` for new installs; check `brew info --cask wireshark-app` if your Homebrew index differs.

If Homebrew is not installed, follow <https://brew.sh/> **or** install Wireshark directly from <https://www.wireshark.org/download.html>.

**Critical — capture permissions:** macOS may require the **ChmodBPF** component to grant access to packet-capture devices. If Wireshark does not show usable interfaces or reports a permissions error, follow the official macOS installer / Homebrew cask guidance to run the **Install ChmodBPF** package and follow its prompts. Log out/in or restart if requested. **Do not run the entire Wireshark GUI with `sudo` as a workaround.**

### Ubuntu 22.04 / 24.04 LTS

Open Terminal:

```bash
sudo apt update
sudo apt install wireshark -y
```

If asked **“Should non-superusers be able to capture packets?”**, choose **Yes** for your own lab machine. If you chose No or missed the question, configure it:

```bash
sudo dpkg-reconfigure wireshark-common
```

Then add your user to the capture group:

```bash
sudo usermod -aG wireshark "$USER"
```

**Log out and log back in** before testing. This group has powerful capture access; use only on a computer you are authorized to administer. Do **not** launch the Wireshark graphical application as root.

If you are on another Linux distribution, use its official packages and the Wireshark permissions instructions rather than blindly running Ubuntu commands.

## 6. Verify Packet Tracer — REQUIRED

1. Open Packet Tracer and complete Cisco sign-in.
2. From the bottom device palette, place **one 2960 switch and two PCs** onto a blank topology.
3. Connect each PC to the switch with copper straight-through connections (the automatic connection option is also acceptable).
4. Configure the interfaces:

   | Device | IPv4 address | Subnet mask |
   |---|---|---|
   | PC-A | `192.168.10.10` | `255.255.255.0` |
   | PC-B | `192.168.10.20` | `255.255.255.0` |

5. No default gateway is needed for these two PCs on the same subnet.
6. Wait for the switch links to become active.
7. On PC-A, open **Desktop → Command Prompt**, then run:

```text
ping 192.168.10.20
```

8. Confirm that packets are received (the **first** ping may time out during ARP learning; retry).
9. Switch to **Simulation Mode** and observe ICMP / ARP events.
10. Save the topology as `lab000_first_network.pkt`.

**Pass condition:** Packet Tracer opens, sign-in succeeds, and the PCs can ping each other.

## 7. Verify Wireshark — REQUIRED

Wireshark will capture traffic from your **real** laptop/desktop, not the two simulated Packet Tracer PCs.

1. Launch Wireshark.
2. Choose an **active** interface, such as Wi-Fi or Ethernet (not necessarily `lo`/loopback).
3. Start a packet capture.
4. Generate traffic in a separate terminal:

**Windows PowerShell**

```powershell
ping -n 4 1.1.1.1
```

**macOS / Linux Terminal**

```bash
ping -c 4 1.1.1.1
```

5. In Wireshark's display filter field, enter:

```text
icmp
```

6. Look for ICMP echo requests (and echo replies if the network permits them). You can also clear the filter and verify that other traffic is captured.
7. Stop capture and save as `lab000_capture.pcapng`.

**Pass condition:** At least one live packet appears on the selected interface. ICMP may be blocked on school/work networks, so a missing reply by itself is **not** proof of installation failure. Try a different active interface or generate DNS/HTTPS traffic if needed.

> **Privacy:** Packet captures can contain hostnames, IP addresses, and sensitive network metadata. **Do not upload an unrestricted live packet capture to a public GitHub repository.** The instructor only needs screenshots and a short summary for Lab 000 unless explicitly requesting a safe, sanitized capture.

## 8. Submission checklist

Submit a short `lab000_report.md` with:

- [ ] Operating system and version (Windows/macOS/Ubuntu)
- [ ] Processor architecture (`x86-64` or `ARM64`, if known)
- [ ] Installed Packet Tracer version and successful Cisco login (screenshot)
- [ ] Screenshot of `lab000_first_network.pkt` showing two PCs and the switch
- [ ] Screenshot of successful ping **inside Packet Tracer**
- [ ] Installed Wireshark version (screenshot)
- [ ] Screenshot of a **real** Wireshark capture with at least one packet visible
- [ ] Any installation errors and the steps attempted to resolve them

Save `lab000_first_network.pkt` in your lab folder. Do not include passwords, authentication tokens, or full public packet captures in your submission.

## 9. Common problems

| Problem | Check / next action |
|---|---|
| Packet Tracer download unavailable | Sign in to Cisco/NetAcad and enroll in the free introductory course; use the official Resource Hub. |
| Packet Tracer asks for login | Use your Cisco/NetAcad account. This is normal. |
| Packet Tracer does not launch on ARM Mac | Check current compatibility; report macOS version and chip to the instructor. Don't use third-party repacks. |
| Ubuntu `.deb` installation fails | Verify supported Ubuntu version and exact filename; use `sudo apt install ./<downloaded-file>.deb`; preserve the error message. |
| `choco` or `brew` not found | The package manager is optional. Use official installers or install the package manager from its official site. |
| Wireshark shows no Windows interfaces | Check Npcap installation, then restart Wireshark / computer if needed. |
| Wireshark shows macOS permission errors | Install/enable ChmodBPF through the trusted installer workflow. |
| Wireshark shows Linux permission errors | Check `wireshark` group membership and log out/in. |
| Packet Tracer ping initially fails | Wait for links and retry; first packet can be delayed by ARP. Check addressing and cabling. |
| Wireshark shows no `icmp` packets | Confirm correct interface; try other traffic and check firewall or network restrictions. |

## 10. Authoritative resources

- [Cisco — Getting Started with Packet Tracer](https://www.netacad.com/courses/getting-started-cisco-packet-tracer/1000)
- [Cisco — Official Resource Hub / Packet Tracer downloads](https://www.netacad.com/resources/lab-downloads)
- [Cisco — Packet Tracer installation guide (PDF)](https://www.netacad.com/skillsforall/files/Cisco_Packet_Tracer_Download_and_Installation_Instructions.pdf)
- [Wireshark — Official downloads](https://www.wireshark.org/download.html)
- [Chocolatey — Wireshark package](https://community.chocolatey.org/packages/wireshark)
- [Homebrew — Wireshark app cask](https://formulae.brew.sh/cask/wireshark-app)
- [Wireshark — User Guide](https://www.wireshark.org/docs/wsug_html_chunked/)

---

**Lab 000 is complete only when both applications open and you can demonstrate simulated connectivity in Packet Tracer and live packet capture in Wireshark.**
