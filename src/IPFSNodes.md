# DECA's IPFS Nodes Setup Guide
The following guide is on how to setup an IPFS node for DECA Protocol Requirements if you want to contribute and provide some infrastructure. This guide is based on Debian 12.1, improvements to our documentation are welcome.

## IPFS Instalation 

1. Download the Linux Kubo binary from [`dist.ipfs.tech`](https://dist.ipfs.tech/#kubo).

   ```bash
   $ wget https://dist.ipfs.tech/kubo/v0.22.0/kubo_v0.22.0_linux-amd64.tar.gz
   ```

1. Untargz the file:

   ```bash
   $ tar -xvzf kubo_v0.22.0_linux-amd64.tar.gz
   > x kubo/LICENSE
   > x kubo/LICENSE-APACHE
   > x kubo/LICENSE-MIT
   > x kubo/README.md
   > x kubo/install.sh
   > x kubo/ipfs
   ```

1. Move into the `go-ipfs` folder and run the install script:

   ```bash
   $ cd kubo

   $ sudo bash install.sh

   > Moved ./ipfs to /usr/local/bin
   ```

1. Test that IPFS has installed correctly:

   ```bash
   ipfs --version

   > ipfs version 0.22.0
   ```

## Setup ipfs service for deca

First time config setup for a server:
   ```sh
      ipfs init --profile server
   ```
> This removes local discovery requests

### Setup Circuit Relay V2
Add swarm address in the config (specifically the ws line):
   ```sh
       "Swarm": [
         "/ip4/0.0.0.0/tcp/4001",
         "/ip4/0.0.0.0/tcp/4004/ws",
         "/ip6/::/tcp/4001",
         "/ip4/0.0.0.0/udp/4001/quic",
         "/ip6/::/udp/4001/quic"
       ]
   ```

Enable Swarm.RelayService with the following command:
   ```sh
      ipfs config --json Swarm.RelayService.Enabled true
   ```

and

   ```sh
      ipfs config --json Swarm.RelayClient.Enabled true
   ```

## Set IPFS as a daemon and Nginx Reverse Proxy
### Set IPFS as a daemon

Copy the following lines after the `sudo vim... command`, modify user and path to ipfs so that it matches with your system and user that runs ipfs: 

   ```sh
    $ sudo vim /etc/systemd/system/ipfs.service
   
   [Unit]
   Description=IPFS Daemon
   
   [Service]
   ExecStart=/usr/local/bin/ipfs daemon --enable-pubsub-experiment
   User=nodemaster
   Restart=always
   LimitNOFILE=10240
   
   [Install]
   WantedBy=multi-user.target
   ```

   **NOTE: in this example user that runs ipfs is nodemaster, also the ipfs location is at /usr/local/bin/ipfs if you don't know the path, try `$ whereis ipfs`**

Enable the service

   ```sh
    $ sudo systemctl daemon-reload
    $ sudo systemctl enable ipfs.service
    $ sudo systemctl start ipfs.service
    $ sudo systemctl status ipfs.service
   ```
   **NOTE: service must be set as active (running), if not please verify the preview steps**

### Nginx Reverse Proxy for a public gateway and websocket 

The Gateway setup:
Change the server name for your own domain name:
   ```sh
   server {
       listen 80;
       server_name gateway.decentralizescience.org;

       location / {
           proxy_pass http://localhost:4001;
           proxy_set_header Host $host;
           proxy_cache_bypass $http_upgrade;
           allow all;
       }
   }
   ```
> Note: Remember to enable the service and get ssl with certbot

The enabling Secure WebSocket with nginx:
> NOTE: Change the server name for your own domain name.

   ```sh
   server {
       listen 80; 
       server_name ipfs.decentralizedscience.org;

       location / {
           proxy_pass http://127.0.0.1:4004;
           proxy_http_version 1.1;
           proxy_set_header Upgrade $http_upgrade;
           proxy_set_header Connection "upgrade";
       }
   }
   ```

> NOTE: Remember to enable the service and get ssl with certbot

## Testing

### Verify Secure WebSocket connection
Doing an IPFS ping
   ```sh
   ipfs ping /dns4/ipfs.decentralizedscience.org/443/wss/p2p/12D3KooWQzickgUJ1N9dNZMJpNnFUCHmhndTVgexXnt6dQhPFcEE

   PING 12D3KooWQzickgUJ1N9dNZMJpNnFUCHmhndTVgexXnt6dQhPFcEE.
   Pong received: time=161.27 ms
   Pong received: time=161.13 ms
   Pong received: time=161.55 ms
   ```
Doing a swarm connect
   ```sh
   ipfs swarm connect /dns4/ipfs.decentralizedscience.org/443/wss/p2p/12D3KooWQzickgUJ1N9dNZMJpNnFUCHmhndTVgexXnt6dQhPFcEE

   connect 12D3KooWQzickgUJ1N9dNZMJpNnFUCHmhndTVgexXnt6dQhPFcEE success
   ```

### check the IPFS public Gateway:

Browse by adding `/ipns/deca.eco/` to your gateway address:
> You should see the IPFS official web3 website

Example:
https://gateway.decentralizedscience.org/ipns/deca.eco/

## License

[**GPLV3**](./LICENSE). ?

## Contact.

***Developers***
- [p1r0](mailto:p1r0@nethunters.xyz)

## ToDo/Proposal

* Setup a DECA testnodes health by forking [this code](https://github.com/ipfs/public-gateway-checker)
* Setup and handle data with [ipfs-cluster](https://ipfscluster.io/)


## References

1. [Install IPFS Kubo](https://docs.ipfs.tech/install/command-line/#install-official-binary-distributions)
2. [file transfer](https://github.com/ipfs/go-ipfs/blob/master/docs/file-transfer.md)
3. [circuit relay](https://docs.libp2p.io/concepts/circuit-relay/)
4. [understanding circuit relay](https://blog.aira.life/understanding-ipfs-circuit-relay-ccc7d2a39)
5. [experimental features](https://github.com/ipfs/go-ipfs/blob/master/docs/experimental-features.md)


