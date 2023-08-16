# simple-taiko-pool-prover

This is a Taiko pool prover docker package, which allow you to join the Davaymne Taiko pool with awesome prove-runners.

Your node will be added in the list of nodes which will be randomly selected to prove Taiko blocks.

Requirements:
 - CPU: Intel i9-12900K or AMD 9550x or similar, should be CPU with more than 3500 Mhz
 - Modify .env with your prover's **public** IP address and port
 - Check that port is open on your firewall.

How to run:
 - Copy `.env.sample` to `.env` and modify `.env` accordingly:
   - Set `PROVER_ENDPOINT` should be in format "IP:PORT", e.g. 8.8.8.8:9000
   - Set `PROVER_PORT` should be equal to port above
   - Set `PROVER_WALLET` it will be used to distribute rewards if block which is generated by your node is accepted by taiko smartcontract
 
> NOTE: taiko-pool is currently in beta version, so rewards are not guaranteed 
  
 - Run docker-compose by `docker-compose up -d`

Note:
 - Upon image update you will need to delete old image to be able to use new one `docker image rm davaymne/taiko-pool-proverd`

How it works:

Once you configure your endpoint and start docker, client will be sending periodic register messages with your public Endpoint and wallet address to the Pool Manager.
Pool manager will assess your node against HW requirements and if it meets will be added in the list of Provers then.
Once new block which requires prove is detected, prover endpoint will be selected from the list and get assigned block to prove.
Prover generate prove and submit it to Taiko Pool, which will be submitted to the contract using Pool Wallet.

Rewards:

 - Dashbord to see your proved blocks - WIP
 - On weekly basis rewards will be distributed on the provided wallets - WIP
