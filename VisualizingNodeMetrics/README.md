# Visualizing Node Metrics
This tutorial builds on previous one, so we need functional Substate template node.

We need to install Grafana and Prometheus. 

First we need to start the node: 
`./target/release/node-template purge-chain --dev -y`

Now when it is working, we need to start the prometheus (preferrebly in Docker container) and modify the `prometheus.yml` file. 
`docker run -p 9090:9090 -v /path/to/file/prometheus.yml:/etc /prometheus/prometheus.yml prom/prometheus`

This was a bit challenging due to my setup - Windows and WSL2.
To add the port and address to the Windows host, I have to add the follwoing firewall rule: 
`netsh interface portproxy add v4tov4 listenport=9090 listenaddress=0.0.0.0 connectport=3000 connectaddress=<ip>`

![It works](https://github.com/pannetusil/polkadot_hack/blob/main/figs/Tut2_response.PNG)


## Resources
[1] https://www.nextofwindows.com/allow-server-running-inside-wsl-to-be-accessible-outside-windows-10-host
[2] https://stackoverflow.com/questions/49835559/how-to-access-to-the-web-server-which-running-on-wslwindows-subsystem-for-linux
[3] https://docs.docker.com/desktop/windows/wsl/
[4] https://prometheus.io/docs/prometheus/latest/installation/
[5] https://grafana.com/grafana/?pg=get&plcmt=selfmanaged-box1-cta1