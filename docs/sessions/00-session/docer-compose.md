❯ I want to set up this codebase as a docker container in my unraid server. What I want specifically is to host my own open source free realms server. While conserving tokens, use a targeted           
  approach to introduce me to the main steps for accomplishing this. I have never used docker manually before.                                                                                          
                                                                                                                                                                                                         
⏺ Read 1 file (ctrl+o to expand)                                                                                                                                                                         
                                                                                                                                                                                                         
⏺ Good. Here's a targeted overview of the main steps:                                                                                                                                                    
                                                                                                                                                                                                         
  ---                                                                                                                                                                                                    
  Overview: Hosting Sanctuary on Unraid via Docker                                                                                                                                                       
                                                                                                                                                                                                         
  The project already has a docker-compose.yml and two Dockerfiles — so the heavy lifting is done. You have two paths:                                                                                   
                  
  Path A: Docker Compose (Recommended — simplest)

  Unraid supports Docker Compose via the Community Applications (CA) plugin → Compose Manager.

  Steps:
  1. Install CA plugin on Unraid if not already installed (search "Community Applications" in Unraid's Apps tab)
  2. Install Compose Manager from CA
  3. Copy your project to Unraid (e.g. via SMB share or scp) — put it somewhere like /mnt/user/appdata/sanctuary/
  4. Create the stack in Compose Manager pointing to your src/Docker/docker-compose.yml
  5. Start the stack — it will build the images and launch both services

  That's essentially it for basic functionality. The compose file already handles:
  - Port mappings (UDP 20041, 20042 for Login; UDP 20260 for Gateway)
  - SQLite database at /data/sanctuary.db inside a bind-mounted .local_data/ folder
  - Shared log volume
  - A Resources/ bind mount (you'll need to populate this — check what goes in src/Docker/Resources/)

  ---
  Path B: Pre-build images, push to registry, use Unraid UI

  More work — only useful if you want to avoid building on Unraid. Compose Manager is much simpler.

  ---
  Key things to verify before starting:

  1. Resources folder — check what src/Docker/Resources/ needs to contain (game data files?)
  2. Ports open — ensure your router/firewall allows UDP 20041, 20042, 20260 if clients are connecting externally
  3. Default admin account — the README notes a default admin/admin user should exist in the DB; verify it's there after first launch

  ---
  Want me to look at what belongs in the Resources/ directory, or help you with any specific step?