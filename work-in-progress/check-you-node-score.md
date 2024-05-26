# Check you node score

Score is the metric: how long it takes to complete 10,000 iterations of the verifiable delay proof

If you check your peer manifest info you can see what your difficulty metric came out to, it's in milliseconds

Where do i go to see the peer manifest info?

you need to convert your peer id: echo “your “peer id | base58 -d | base64 then use that output and call grpcurl -plaintext localhost:8337 quilibrium.node.node.pb.NodeService.GetPeerManifests | grep -A 15
