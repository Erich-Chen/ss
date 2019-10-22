# ss

```

sudo apt update
sudo apt install shadowsocks



cat << EOL | sudo tee /ss/ss.json
{
    "server": "::",
    "timeout": 60,
    "method": "aes-256-cfb",
    "port_password": {
        "1234": "passw0rd",
        "4567": "pa$$word"
    }
}
EOL



cat << EOL | sudo tee /etc/systemd/system/shadowsocks-server.service
[Unit]
Description=Shadowsocks Server
After=network.target
[Service]
ExecStart=$(which ssserver) -c /ss/ss.json
Restart=always
[Install]
WantedBy=multi-user.target

EOL



sudo systemctl daemon-reload
sudo systemctl enable shadowsocks-server.service
sudo systemctl start shadowsocks-server.service
sudo systemctl status shadowsocks-server.service


# reboot

```
