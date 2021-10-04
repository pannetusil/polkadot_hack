
prometheus.yml

sudo docker run -p 9090:9090 -v /home/filipebek/Documents/Hackathons/Polkadot/prometheus.yml:/etc
/prometheus/prometheus.yml prom/prometheus

https://www.nextofwindows.com/allow-server-running-inside-wsl-to-be-accessible-outside-windows-10-host
https://stackoverflow.com/questions/49835559/how-to-access-to-the-web-server-which-running-on-wslwindows-subsystem-for-linux
https://docs.docker.com/desktop/windows/wsl/

https://prometheus.io/docs/prometheus/latest/installation/
https://grafana.com/grafana/?pg=get&plcmt=selfmanaged-box1-cta1

netsh interface portproxy add v4tov4 listenport=9090 listenaddress=0.0.0.0 connectport=3000 connectaddress=172.31.232.189