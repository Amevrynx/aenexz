SecureCorp — Week 1 Working Evidence

CONFIRMED LAB DETAILS
- Arch Linux physical/libvirt host: 192.168.1.8
- Ubuntu libvirt VM: 192.168.122.138/24
- Kali libvirt VM: 192.168.122.139/24
- Lab gateway: 192.168.122.1
- Lab VM network: 192.168.122.0/24
- Wazuh Manager + Dashboard: Arch host
- Ubuntu: DVWA target + Wazuh agent
- Kali: authorized analyst/attacker VM + Wazuh agent


The network diagram keeps the Arch host outside the 192.168.122.0/24 VM subnet and represents Ubuntu/Kali as libvirt guests. No unverified NAT/bridge details are asserted.