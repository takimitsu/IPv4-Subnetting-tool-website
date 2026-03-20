# IPv4 Subnet Calculator
A lightweight, JavaScript-based tool designed to calculate network details on an IPv4 address and a CIDR subnet mask. This tool helps users determine the network range, usable host addresses, and whether an IP address is public or private.
## Features
* **Network Address Calculation**: Determines the base network address.
* **Usable Host Range**: Calculates the first and last usable IP address within the subnet.
* **Broadcast Address**: Identifies the broadcast address for the given network.
* **Subnet Mask Conversion**: Converts CIDR notation into dotted-decimal subnet mask.
* **Host Count**: Calculates the number of usable hosts (using the 2^n - 2 formula).
* **IP Classification**: Detects if the provided IP falls under Class A, B, or C private ranges or is a Public IP.
* **Binary Visualization**: Displays the IP address in binary format before and after the mask is applied.
## How it works
The script processes user input through several functions:
1. `calculate()`: Handles DOM manipulation, validates that the inputs are numbers between 0-255 (and masks 0-32), and performs the binary string slicing.
2. `ip_status(part1, part2)`: Checks the first two octets against RFC 1918 standards to classify the address.
3. `add_padding(octet)`: Ensures every binary octet is exactly 8 bits long by adding zeros where necessary.
4. `subnet_zeros(subnetMask)`: Generates the full 32-bit binary string for the subnet mask.
5. `calculate_hosts(subnetMask)`: Uses the remaining bits (32 - mask) to calculate the total capacity of the subnet.
## IP Classifiation Logic
The tool identifies private networks based on the following criteria:
| Range | Class | Type |
| :--- | :--- | :--- |
| `10.0.0.0` - `10.255.255.255` | Class A | Private |
| `172.16.0.0` - `172.31.255.255` | Class B | Private |
| `192.168.0.0` - `192.168.255.255` | Class C | Private |
| Everything else | N/A | Public |
## Setup and Usage
### Prerequisites
An HTML file containing inputs with the following IDs:
* `part1`, `part2`, `part3`, `part4` (IP octets)
* `subnetpart` (CIDR mask)
* Various `id` tags for result display (e.g., `network-address`, `available-hosts`, etc.)
### Execution
Simply call the `calculate()` function (via a button click on the site) after filling in the fields.
```html
<button onclick="calculate()">Calculate Subnet</button>
```
## Known Limitations
Since this is an older project which hasn't been maintained and was built when I had less coding skills, it has limitations.
* Subnet /32 and /31: The current usable host calculation (2^n - 2) may return `0` or `-1` for /32 and /31 masks, which is correct but behaves differently in specific scenarios.
* UI Dependency: The script is tightly coupled with specific DOM element IDs and expects them to exist to fuction without errors.
## License
This project is open-source and available under the MIT License.
