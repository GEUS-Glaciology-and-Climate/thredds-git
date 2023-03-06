# thredds-git

All files in this repo are for controlling the THREDDS data server, located at:

https://thredds.geus.dk

The Azure THREDDS VM uses symlinks between files at the `/data/content/thredds` location to files in this repo.
Files should be edited in the cloned repo at `/data/thredds-git`, and any changes will automatically be used on the production
THREDDS site via the symlinks.

You must shutdown and restart the Tomcat web server for any changes to take effect:

```
root@thredds:/opt/tomcat/bin# ./shutdown.sh
root@thredds:/opt/tomcat/bin# ./startup.sh
```

The cloned repo at the Azure THREDDS server is setup using [git deploy keys](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/managing-deploy-keys#deploy-keys). The public and private ssh keys and the `config` file for the server are located at `/root/.ssh`. The remote on the cloned repo (`git remote -v`) is then configured as `git@github.com-thredds-git:GEUS-Glaciology-and-Climate/thredds-git.git`. Because the public key is registered with this repo on github (write access), any git commands from the Azure THREDDS server will have access.

Due to permission conventions at `/data` on the Azure THREDDS server, all edits to files in this repo must be made as the `root` user (`sudo su`). This could be changed if desired (e.g. give the `aws` user write permissions).
