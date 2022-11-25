# Docker Notes

## Move Docker data directory to another location on ubuntu

* Stop docker daemon
```bash
sudo service docker stop
```
* Add a docker configuration file to tell docker daemon what is the location of the data directory, this files is located at ``/etc/docker/daemon.json`` but it's not there create a new one and add the following configuration.
```bash
{
  "data-root": "/path/to/your/docker"
}
```
* Copy the current data to the new one
```bash
sudo rsync -aP /var/lib/docker/ /path/to/your/docker
```
* Rename the old docker directory
```
sudo mv /var/lib/docker /var/lib/docker.old
```
* Restart docker daemon
```bash
sudo service docker start
```
* If everything is ok remove the old docker directory
```bash
sudo rm -rf /var/lib/docker.old
```