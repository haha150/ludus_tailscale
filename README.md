# ludus_tailscale
Ansible Role for Ludus to provision or remove a device to/from a Tailnet.
## REQUIREMENTS
- Requires Ludus 1.5.4 or greater as this version and above contain improvements in IP determination within the Dynamic Inventory steps which affect how Ludus operates in a Tailscale environment.
- Tailscale authorization key which is configured for reuse if going to be used for more then one VM.
- Tailscale API key with permissions to remove devices.
## Installation Instructions
### To Install with ansible galaxy
```
ludus ansible role add haha150.ludus_tailscale
```
- If you install from this method, in your range config the role name should be "haha150.ludus_tailscale"
### To Install from this git repo
- Clone this repo
```
git clone https://github.com/haha150/ludus_tailscale.git
```
- add it to ludus roles
```
ludus ansible role add -d ./ludus_tailscale
```
## Role Variables
```
tailscale_state: present/absent
tailscale_authkey: "tskey-auth-<REDACTED_KEY>"
tailscale_api_key: "tskey-api-<REDACTED_KEY>"
tailscale_ssh: true/false
tailscale_dns: true/false
tailscale_advertise_routes:
  - <IP_ADDRESS>/24
```
## Deploy role
- set your config like the one in the example ludus-config.yaml
  - Ensure your api key is for a user with permissions to remove devices from the tailnet.
  - ensure auth key is valid
- either deploy whole range with
```
ludus range deploy
```
- or deploy just tailscale role
  - Useful for deploying tailscale to existing vm's or removing tailscale from existing VM's.
  - **Hint**: can be used with "absent" as the tailscale state variable value to purge tailscale prior to destroying range.
```
ludus range deploy -t user-defined-roles --only-roles <ludus_tailscale| haha150.ludus_tailscale>
```
