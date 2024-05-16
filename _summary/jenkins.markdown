```bash
sudo apt install openjdk "unable to locate package openjdk"
sudo apt search openjdk
sudo apt install openjdk-11-jre-headless
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt update
sudo apt install jenkins
sudo service jenkins status | less
netstat -an | less
curl ifconfig.me
sudo usermod -aG docker jenkins
```
