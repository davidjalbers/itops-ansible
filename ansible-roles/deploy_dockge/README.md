# deploy_dockge

This role is used to deploy **dockge** with Docker Compose.

Note that this role only creates the necessary files and directories, and does not actually run the application. 
To start dockge, you need to run `docker compose up -d` in `/opt/dockge` (where `compose.yaml` is located).
This is because the first time you run dockge, the web interface will offer the possibility create the superuser and this is something that shouldn't be automated.
