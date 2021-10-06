# Visualizing Node Metrics - https://substrate.dev/docs/en/tutorials/visualize-node-metrics/
This tutorial builds on previous one, so we need functional Substate template node.

We need to install Grafana and Prometheus. 

First we need to purge all content and start the node: 
`./target/release/node-template purge-chain --dev -y`
`./target/release/node-template --dev --tmp`

Now when it is working, we need to start the prometheus (preferrebly in Docker container) and modify the `prometheus.yml` file. 
`docker run -p 9090:9090 -v /path/to/file/prometheus.yml:/etc /prometheus/prometheus.yml prom/prometheus`

This was a bit challenging due to my setup - Windows and WSL2.
At the end, the best way is to setup a remote desktop session and connect to the WSL2. 
Now, we start the Grafana, login, and enhance the dashboard provided by Substrate
`sudo service grafana-server start`

![It works](https://github.com/pannetusil/polkadot_hack/blob/main/figs/Tut2_response.PNG)
![It works](https://github.com/pannetusil/polkadot_hack/blob/main/figs/Tut2_dashboard.PNG)


## Resources
[1] https://www.nextofwindows.com/allow-server-running-inside-wsl-to-be-accessible-outside-windows-10-host
[2] https://stackoverflow.com/questions/49835559/how-to-access-to-the-web-server-which-running-on-wslwindows-subsystem-for-linux
[3] https://docs.docker.com/desktop/windows/wsl/
[4] https://prometheus.io/docs/prometheus/latest/installation/
[5] https://grafana.com/grafana/?pg=get&plcmt=selfmanaged-box1-cta1
[6] https://www.nextofwindows.com/how-to-enable-wsl2-ubuntu-gui-and-use-rdp-to-remote