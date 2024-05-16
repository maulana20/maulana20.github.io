```bash
sudo apt install docker.io
sudo usermod -aG docker $USER
sudo service docker start
docker version
ls -l /var/run/docker.sock
sudo chmod 666 /var/run/docker.sock
```
