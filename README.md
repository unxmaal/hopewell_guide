# 15444 Hopewell Road Guide

## House Systems

### Water System
- **Source**: Private Well
- **Location**: Under a concrete cover below the large retaining wall southeast of the gravel parking area
- **Maintenance**:
	- Annual testing of well water is recommended by the State of Georgia
	  - Yearly sterilization with chlorine is advised
- Water heater
	- @2015 80 gallon Whirlpool E2F80HD045V
	- serial number 1503100820069 
	- elements replaced 2020
	- serviced 12/10/24
	- Note it's important to drain and flush this water heater once per year.
		- Turn off the breaker
		- Attach garden hose to drain port at the bottom
		- Run hose out a basement door
		- Drain

### Septic System
- **Location**: Northeast corner in front of the house
- **Usage Guidelines**:
  - Only human waste should enter the system
  - Do not dispose of:
    - Food (even from a sink garbage disposal, which is why there isn't one)
    - Feminine hygiene products
    - Chewing gum
    - Thick, triple-ply toilet paper
    - Chlorine bleach
- **Maintenance**:
  - Treat monthly with Pro Pump Septic Saver (small dry packet)
  - Flush a bottle of "Hi Count" liquid if a large amount of bleach enters the system or after yearly well sanitization
  - Last pumped in 2023 (drain field lines cleaned at this time)
  - Next pump and cleanout due in 2027; obtain quotes before problems arise

### Electrical System
- **Recent Updates**:
  - Updated to 2022 Code in 2023 by TE Certified
  - Improvements include:
    - 4-wire service from mains to meter
    - New service mast and meter
    - New external full-system shut-off breaker
    - Replacement of main panel and adjacent subpanel
    - All breakers replaced with arc-fault breakers
    - All circuits traced and labeled
    - Whole-house surge protectors for all 3 panels
- **Panel Locations**:
  - **Main Panel**: Basement mechanical room
  - **Subpanel 1**: Next to the main panel in the mechanical room
  - **Subpanel 2**: Garage

### Heating and Cooling Systems
- **Central HVAC**:
  - 5.5-ton unit controlled by a Nest thermostat
  - 2 Nest remote sensors 
	  - Best positioned in Master Bedroom and in the Living Room (or wherever you spend your time during the day)
	  - Configure the Nest to use the MBR sensor in the evenings, and the LR sensor during the day
  - Serviced in 2023
  - Vent settings
	  - Set both vents in MBR to half open
	  - Set the vent in the hallway bedroom to 1/4 open
	  - Set the vent in the other bedroom to half open
	  - Set the LR vents to full open
	  - Set the basement vents to full open (debatable)
- **Mini-split Systems**:
  - More efficient than the central unit (saves approximately $200/month in power usage during winter and summer)
  - One exterior unit with two head units (Kitchen and Classroom)
  - Controlled by remote units stored in the kitchen island drawer
- **Wood Burning Stove**:
  - Requires yearly service (Vendor: The Mad Hatter)
  - Use a pot full of water on top to maintain house humidity levels
- Jumper Ducts
	- 2 ducts in the living room ceiling to circulate hot air to the kitchen and master bedroom
	- Fan switches located in:
	    - Master bedroom near the smaller closet
	    - Kitchen near the refrigerator

### Security System
- **System**: Ring Security
	- **Components**:
	    - Base station
	    - Two panels (one in the basement and one in the classroom)
	    - Contact sensors on all doors
	    - Motion detectors in the kitchen and basement
	    - First Alert smoke and CO detectors in each bedroom and hallway (per GA Code)
	    - Water/freeze sensors
	    - 2 doorbell cameras
	- New setup
		- This system and all devices should be in default configuration
		- Install the Ring app, then add the base station, then add each device
		- Add the smoke detectors

### Drainage Systems
- Gutters
	- The gutters _must_ be cleaned out at least twice a year, preferably in December and in May
	- James Lockwood, (770) 789-1606, $250

-----

## Service Providers
### Power
- **Provider**: Sawnee EMC
### Internet
- **Provider**: Xfinity
### Termite Bond and Pest Control
- **Provider**: Breda Pest
### Trash
- **Provider**: Republic Services
### Landscaping
- **Provider**: Keith Berne
  - **Contact**: (404) 513-8114
  - **Background**: Keith owned this property for over 10 years and handled most of the original landscaping

--------
## Network Setup

## Ethernet wiring

- The Xfinity drop is in the living room in the corner
- I installed the modem, router/firewall, and a switch there
- Ethernet runs
	- LR to basement
	- LR to classroom/den
	- Basement corner to Master Bedroom
		- 3 ports going to:
			- ethernet port near the ceiling
			- MBR near the floor
			- MBR near ceiling
		- The higher ports are for the radios
		- I used a POE switch here

## Installing and Configuring UniFi Controller on Raspberry Pi Using Docker

### Prerequisites

- Raspberry Pi with an up-to-date OS (e.g., Raspberry Pi OS Lite).
- Docker and Docker Compose installed.
- Internet connection.
- SSH access to the Raspberry Pi (optional but recommended).

### Steps

### 1: Update and Prepare the Raspberry Pi
sudo apt update && sudo apt upgrade -y
sudo apt install curl -y

### 2: Install Docker and Docker Compose

```

#install Docker
curl -fsSL https://get.docker.com | sh

#### Add the current user to the Docker group (replace <your-username> with your username)
sudo usermod -aG docker <your-username>

# Install Docker Compose
sudo apt install -y docker-compose

# Reboot the Raspberry Pi to apply changes
sudo reboot
```
### 3: Create the Docker Compose Configuration

```

# Create a working directory
mkdir ~/unifi-controller && cd ~/unifi-controller

# Create a docker-compose.yml file
nano docker-compose.yml

# Add the following configuration
# ---------------------------------
# version: '3.8'
# services:
#   unifi-controller:
#     image: ghcr.io/linuxserver/unifi-controller:latest
#     container_name: unifi-controller
#     restart: unless-stopped
#     network_mode: host
#     volumes:
#       - ./config:/config
#     environment:
#       - PUID=1000  # Replace with your user ID
#       - PGID=1000  # Replace with your group ID
#       - TZ=Etc/UTC # Replace with your timezone
# ---------------------------------
# Save and exit the file.

# Find your PUID and PGID
id
# Example output: uid=1000(pi) gid=1000(pi)
# Replace PUID and PGID in the docker-compose.yml file with these values.
```

### 4: Start the UniFi Controller

```
# Start the container
docker-compose up -d

# Check the container's status
docker ps
```

### 5: Access the UniFi Controller Web Interface

```
# Open a browser and navigate to:
# http://<Raspberry_Pi_IP>:8443
# Replace <Raspberry_Pi_IP> with your Raspberry Pi's IP address.

# Complete the UniFi setup wizard.
```

### 6: Adopt and Manage UniFi Devices
* Ensure your Raspberry Pi and UniFi devices are on the same network.
- Reset your UniFi devices to factory settings.
- Adopt the devices in the UniFi Controller interface.

### 7: Backup and Update
- Backup your configuration regularly through the web interface.
-  To update the UniFi Controller image

```
docker-compose pull
docker-compose up -d
```

### Radio positioning

For best coverage, try the following locations
- Living Room
- Master Bedroom
- Classroom
- Garage 

The Unifi USG radios should be positioned horizontally on ceilings facing down, not vertically attached to walls. 

Wired connections are better, but if ethernet is unavailable (like for the garage), they will connect to each other via mesh networking.  

