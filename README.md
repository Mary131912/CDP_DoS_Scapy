# CDP DoS Attack Script

## Overview
The CDP DoS Attack script simulates a Denial of Service (DoS) attack against Cisco devices using the Cisco Discovery Protocol (CDP). It enables network professionals to understand the implications of CDP vulnerabilities and helps in testing the resilience of network infrastructure.

## Installation Instructions
1. **Clone the repository:**  
   ```bash
   git clone https://github.com/Mary131912/CDP_DoS_Scapy.git
   cd CDP_DoS_Scapy
   ```  
2. **Install requirements:**  
   ```bash
   pip install -r requirements.txt
   ```

## Usage
Run the script using Python 3.x as follows:
```bash
python cdp_dos_attack.py -t <target_ip> -i <interface>
```
### Parameters:
- `-t <target_ip>`: Specify the target IP address.
- `-i <interface>`: Specify the network interface to use.

## Topology
- The attack setup generally includes:
  - A target Cisco device (router/switch).
  - An attacking machine running the script.
  - Proper network connections (through a switch/router for packet delivery).

## Requirements
- Python 3.x
- Scapy library

## Script Code
The script is written in Python and utilizes the Scapy library for packet crafting and sending. Place the code within the `cdp_dos_attack.py` file in this repository.

## Verification Steps
1. Use network monitoring tools to observe traffic.
2. Validate the impact on the target Cisco device.

## Mitigation Measures
- Disable CDP on devices if unnecessary.
- Implement ACLs to limit CDP access.

## Key Concepts
- **Denial of Service (DoS)**: Making a service unavailable to its intended users by overwhelming it with traffic.
- **Cisco Discovery Protocol (CDP)**: A layer 2 protocol used by Cisco devices for network discovery and information sharing.

## Security Considerations
- Use this script in a controlled environment and only with permission, as it can disrupt network operations.

## References
- [Cisco CDP Documentation](https://www.cisco.com/c/en/us/td/docs/internetworking/technology/cdp/guide/cdp_overview.html)
- [Scapy Documentation](https://scapy.readthedocs.io/en/latest/)

## License
This project is licensed under the MIT License.

## Author Information
- Name: Mary131912
- Date: 2026-02-06

---

*Note: Ensure that you have permission to test against the target device.*