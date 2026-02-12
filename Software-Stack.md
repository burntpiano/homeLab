## PiWRT - OS: Openwrt

### Customizations

- Cron job to scrape modem logs via Python for any inconsistencies with cable
  connectivity from ISP downstream
- Changed shell to Zsh from ash (for homogenous shell environment)
- ~~Compiled cmake solely for fastfetch in Zsh~~
  - Sike! Soar PkgForge was easier instead of fixing issues with linkers during
    compiling
- Heavily segmented and firewalled network

## Actual Server Stack - Proxmox

### Services Running

- My static portfolio website is hosted in an Alpine Linux LXC container running
  NGINX (via Docker) served through a Cloudflare Tunnel
  - Port forwards? No thx lol
- Sunshine server for remote desktop accessible via mobile device (laptop,
  phone, handheld emulator, etc.)
- Media acquisition stack
  - Open to interpretation
- Select VMs have Tailscale installed for remote access of host system
- Mirrored 4TB ZFS served to nodes via NFS for VM and LXC monthly backups
- NGINX Proxy Manager for SSL LAN only access to services
- LAN only Home Assistant for home automation
  - Simple toggle switches for bulbs
  - Cat deterrent
