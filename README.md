# skills-compose
Docker Compose setup for a Skills Alberta Competitor machine

## Setup

or, "the steps I took":

1. Follow https://www.youtube.com/watch?v=MJgIm03Jxdo for Ubuntu LTS
2. Assign static IP in Edge Router X on vlan 101
3. `sudo apt install qemu-guest-agent`
4. `sudo nano /etc/ssh/sshd_config.d/60-cloudimg-settings.conf` (change `PasswordAuthentication` to `yes`)
5. `sudo systemctl restart ssh`
6. `sudo reboot` then `ip a` to verify the static IP took

Then, in a jumpbox, create `tmux` windows for each of the hosts (preload `ssh ptc@192.168.101.[51]` command without hitting enter) and `Ctrl+B` `:` then `setw synchronize-panes on`

Then:

1. `Enter` and enter password to start SSH
2. Run https://docs.docker.com/engine/install/ubuntu/
3. `sudo docker run --rm -it hello-world` to verify engine
4. `git clone https://github.com/turt2live/skills-compose.git`
5. `cd skills-compose`
6. `nano compose.yaml` to change `MARIADB_ROOT_PASSWORD` (PMA host will get changed later).
   * Also break out of synchronized panes mode to set `MARIADB_PASSWORD` in each VM.
7. `sudo docker compose build`
8. `sudo adduser skills` and follow prompts:
   * New password: ASSIGN TEMPORARY PASSWORD
   * Full name, etc: whatever
9. `sudo su -l skills`
10. `mkdir website && chmod 775 website`
11. `exit` to get out of skills user
12. `sudo docker compose up`
