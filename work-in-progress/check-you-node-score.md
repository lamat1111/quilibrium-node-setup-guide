# Check you node score

Score is the metric: how long it takes to complete 10,000 iterations of the verifiable delay proof

If you check your peer manifest info you can see what your difficulty metric came out to, it's in milliseconds

Where do i go to see the peer manifest info?

you need to convert your peer id:&#x20;

`echo <your_peer_id> | base58 -d | base64`&#x20;

then use that output and call&#x20;

`grpcurl -plaintext localhost:8337 quilibrium.node.node.pb.NodeService.GetPeerManifests | grep -A 15 <output_here>`



test

```
grpcurl -plaintext localhost:8337 quilibrium.node.node.pb.NodeService.GetPeerManifests | grep -A 15 EiDQRetB3wNzuoy0SZE3oGm5lW+fRHgh6B+3Pd61YZnojA==
```

I always get a  `grpcurl: command not found` on my nodes... \
I have installed both \
\
GO

```
wget https://go.dev/dl/go1.20.14.linux-amd64.tar.gz
sudo tar -xvf go1.20.14.linux-amd64.tar.gz
sudo mv go /usr/local
sudo rm go1.20.14.linux-amd64.tar.gz
sudo nano ~/.bashrc
```

&#x20;and then grpcurl with

```
go install github.com/fullstorydev/grpcurl/cmd/grpcurl@latest
```

and I have these variables in .bashrc

```
export GOROOT=/usr/local/go
export GOPATH=$HOME/go
export PATH=$GOPATH/bin:$GOROOT/bin:$PATH
```
