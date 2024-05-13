<!-- PROJECT LOGO -->
# VMware Virtual Initiative

A collaborative space to aid students launch their very own homelab projects.

<!-- ABOUT THE PROJECT -->
## About The Project

The VI Project offers a guide for creating a homelab environment where students can experiment with various technologies and applications using VMware. By using virtualization technology we aim to reduce entry barriers students may face. The project includes guides, notes, examples, and tools to promote peer-to-peer learning.

**Our Objective** : Help students research and develop IT skills.

<!-- Prerequisites -->
## Prerequisites

1. Verify your CPU can support virtualization.
   - [ ] Intel CPU's uses **VT-x**, **VT-d**
   - [ ] AMD CPU's uses  **AMD-V**
2. Enable Virtualization.
   - [ ] Enable virtualization support in BIOS
     - Reboot your machine and spam click `F2`, `Del`, or `F12` keys to enter BIOS.
     - Navigate through the BIOS Menus and look for Virtualization Support options, Enable them. Below is an example of what one would look like.
     ![Bios Example](/media/images/bios%20(2).JPG)
   - [ ] Verify in Task Manager
    ![Example](/media/images/task%20man1.png)
3. Install/Open your preferred Hypervisor
   - [x] VMware Workstation Pro (Recommended)
   - [ ] VMware player (Free)
   - [ ] Virtual Box (Free/MacOS support)
   - [ ] VMware Fusion (MacOS support)
   - [ ] Hyper-V (Free in Windows Pro/Education/Enterprise)

> **Disclaimer !!!**
The project uses **VMware Workstation v16** running on windows.
Issues/Configurations on Linux, MacOS, VMware Fusion, Hyper-V, and VirtualBox have not be tested. (**Planned for the Future**)

<!-- GETTING STARTED -->
## Getting Started

Start Here for new students -> [Intro to VMware](/labs/Intro_to_VMware.md)

Skip VMware Tutorial -> [Labs](/labs/labs.md)

<!-- TABLE OF CONTENTS -->

<!-- USAGE EXAMPLES -->
## Usage

The repository will contain lab environments, each dedicated to specific experiments.

Every lab and experiment will start with a basic template, which serves two main purposes: it provides a consistent foundation for setting up and repeating experiments.
The goal is to support students learn and collaboration by offering a familiar starting point.

Students are encouraged to identify and solve problems within their virtual environments and to document their processes. This practice helps them enhance their critical thinking and troubleshooting skills, while deepening their knowledge of the technologies in use.

In our weekly meetings, students will present their solutions or insights to the group, fostering a collaborative learning atmosphere. On other days, the sessions will focus on constructing a lab or deploying software, guided by an instructor.

<!-- ROADMAP -->
## Roadmap

- [x] Intro to VMware

- [x] Enterprise Network
  - [x] Smart Cards
  - [ ] Linux Integration
  - [ ] VOIP Deployment
  - [ ] Support Ticketing System
  - [ ] Email Server
  - [ ] NAS Solutions
  - [ ] WebServer Solutions

- [ ] SOHO Network
  - [ ] VPN Solutions
  - [ ] NVR Deployment
  - [ ] NAS Deployment
  - [ ] Yubikey Solutions

- [ ] Linux Only Challenge
  - [ ] Linux Domain Controller

- [ ] Software Tester
  - [ ] IT Support Tools
  - [ ] VSCode Setups
  - [ ] Password Managers
  - [ ] Wireshark

- [ ] Other
  - [ ] SOC
  - [ ] NIST Framework
  - [ ] Splunk
  - [ ] Dashboard
  - [ ] Pen Test

Future features or updates that might be added to the project.

<!-- CONTRIBUTING -->

<!-- LICENSE -->

<!-- CONTACT -->
## Contact

Fabian Quiroz - <fabian.quiroz.tech@gmail.com>

<!-- ACKNOWLEDGEMENTS -->
