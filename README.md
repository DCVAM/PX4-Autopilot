# Drone Control System for Industrial Inspections

This repository contains a simulation environment for developing and testing autonomous drone control systems tailored for industrial inspection tasks using PX4 Autopilot.

## Key Features
- PX4 SITL (Software-In-The-Loop) simulation with Gazebo
- Pre-configured F450 drone model with brushless motors
- Ready-to-use setup for industrial inspection scenarios
- Integration with QGroundControl for mission planning

## Prerequisites
- Ubuntu 20.04/22.04 LTS (Recommended)
- Git
- Gazebo 11+
- PX4 development toolchain
- QGroundControl (for mission control)

## Quick Start Guide

### 1. Setup Workspace
```bash
# Create project directory
mkdir -p ~/drone_ws/src
cd ~/drone_ws/src

# Clone repository with submodules
git clone https://github.com/DCVAM/PX4-Autopilot.git --recursive
cd PX4-Autopilot
```

### 2. Build Simulation Environment
```bash
# Compile SITL with F450 airframe configuration
make px4_sitl gz_f450_brush
```
This command:
- Builds PX4 firmware for simulation
- Launches Gazebo with the F450 airframe
- Automatically starts QGroundControl (if installed)
- Initializes MAVLink connections

### 3. Basic Operations
1. Arm the drone using QGroundControl
2. Take off manually or via mission plan
3. Use the following controls in terminal:
   - `commander takeoff` - Autonomous takeoff
   - `commander land` - Initiate landing
   - `commander arm`/`disarm` - Arm/Disarm motors

## Advanced Configuration
### Custom Missions
1. Create inspection routes in QGroundControl
2. Add waypoints with sensor trigger actions
3. Configure camera/gimbal parameters in:
   ```bash
   ~/drone_ws/src/PX4-Autopilot/ROMFS/px4fmu_common/init.d-posix/airframes/4001_f450_brush
   ```

### Sensor Integration
Add custom sensors to `gz_f450_brush.sdf`:
```xml
<sensor name="inspection_camera" type="camera">
  <update_rate>30</update_rate>
  <camera>
    <horizontal_fov>1.047</horizontal_fov>
    <image>
      <width>1920</width>
      <height>1080</height>
    </image>
  </camera>
</sensor>
```

## Directory Structure
```
PX4-Autopilot/
├── build/          # Compiled binaries
├── launch/         # Simulation launch files
├── models/         # Custom drone models
├── src/            # Firmware source code
└── tools/          # Development utilities
```

## Troubleshooting
- **Build Errors**: Ensure all submodules are initialized (`git submodule update --init --recursive`)
- **Gazebo Crashes**: Verify GPU drivers and Gazebo version compatibility
- **Connection Issues**: Check MAVLink ports in QGroundControl settings

## Contributing
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/inspection-path-planning`)
3. Commit changes (`git commit -m "Add thermal camera simulation"`)
4. Push to branch (`git push origin feature/inspection-path-planning`)
5. Submit pull request

For detailed documentation, visit [Project Wiki](https://github.com/DCVAM/PX4-Autopilot/wiki)

## Changing code and contributing

This [Developer Guide](https://docs.px4.io/main/en/development/development.html) is for software developers who want to modify the flight stack and middleware (e.g. to add new flight modes), hardware integrators who want to support new flight controller boards and peripherals, and anyone who wants to get PX4 working on a new (unsupported) airframe/vehicle.

Developers should read the [Guide for Contributions](https://docs.px4.io/main/en/contribute/).
See the [forum and chat](https://docs.px4.io/main/en/#getting-help) if you need help!

## Project Governance

The PX4 Autopilot project including all of its trademarks is hosted under [Dronecode](https://www.dronecode.org/), part of the Linux Foundation.

<a href="https://www.dronecode.org/" style="padding:20px" ><img src="https://mavlink.io/assets/site/logo_dronecode.png" alt="Dronecode Logo" width="110px"/></a>
<a href="https://www.linuxfoundation.org/projects" style="padding:20px;"><img src="https://mavlink.io/assets/site/logo_linux_foundation.png" alt="Linux Foundation Logo" width="80px" /></a>
<div style="padding:10px">&nbsp;</div>


## License
This project is licensed under the BSD 3-Clause License - see the [LICENSE.md](LICENSE.md) file for details

