## Planned Services

- faster-whisper to detach from Amazon's ecosystem
  - Various Raspberry Pi Zeros would be strategically located with ReSpeaker
    HATs that would serve as Wyoming Satellites
- Motherboard swap for dual GPU compatability
- NVIDIA Enterprise vGPU driver patch for VRAM slicing
  - This is primarily due to budgetary restraints, however, owning two Turing
    architecture GPUs is ideal for this approach
- Expanding automations with Home Assistant
  - Presence detection via nmap to power on/off the server stack via Wake-on-LAN
    - nmap is preferred over "true" geofencing integrations as they are not kind
      to phone batteries
  - BLE beacons and recievers for presence detection
