# Cardano-Node
We are going to build a Cardano Node! 

What is Cardano?
Cardano ($ADA) is a 3rd-generation cryptocurrency (similar to Bitcoin and Ethereum, but different in many ways) that aims to be the most decentralized cryptocurrency that will benefit the world. Cryptocurrencies are all racing to bring the revolutionary technology of blockchain to the real world. A blockchain is simply a ledger (or list of transactions) that are powered by a bunch of connected computers. The blockchain is decentralized (not owned by a single entity/person) and powered by many (connected nodes/computers). The Bitcoin/Ethereum network is powered by a bunch of computers connected together.

The Bitcoin and Ethereum blockchain operates as Proof-of-Work while the Cardano blockchain operates as Proof-of-Stake. 

What is Proof-of-Work? Proof-of-Work simply means that miners (aka Computers with [sold out] GPUs) WORK to solve complex problems and these complex problems validate the network and it's transactions. The miner that successfully solves the problem gets rewards with Bitcoin/Ethereum. Hence, Proof-of-WORK. This is a very energy-intensive process and will only keep increasing as demand continues to grow for cryptocurrency.

What is Proof-of-Stake? Proof-of-Stake means that validators/stakers (aka people with an X amount/stake of $ADA) can use their current X amount of $ADA to validate the network. Stakers have a choice of running their own node which connects directly to the Cardano blockchain or to "delegate" their stake/amount of $ADA to a node. Stakers then earn a reward for validating the network. Staking requires a lot less energy than Proof-of-Work cryptocurrencies. 

So today, we will be building up a Cardano Node on AWS.

# Useful Links
1. Cardano homepage to learn more: https://cardano.org/
2. Cardano-Node instructions: https://cardano-community.github.io/guild-operators/#/README
3. AWS Platform to host our node: https://aws.com

# Create an EC2 Instance on AWS
1. Create an EC2 instance with Ubuntu (I used Ubuntu Server 20.04 LMS)
2. Select t2.medium and for 24-30 GB for EBS Storage
3. We can leave default VPC and Security Group for now (will be a security risk if not addressed later since it is open to the world!)
4. Tag it! (i.e., Name, CardanoNode) 
5. Save your Private Key (i.e., mykeypair.pem) so that you can connect to it later

# Connect into your Cardano Node
1. You can choose whatever SSH method you like, I am running on Windows and my command line has SSH configured. Let's SSH into our Ubuntu Server using the server's public IP address and our generate private key (mykeypair.pem) as ubuntu (default AWS account user for Ubuntu)  
ssh ubuntu@12.345.678.90 -i mykeypair.pem  
yes  
2. Once connected, lets update the server!  
sudo apt-get update

# Secure your Cardano Node
1. Check firewall (ufw) status  
sudo ufw status  
2. Set your firewall configuration  
sudo ufw allow proto tcp from any to any port 22  
3. Allow node port  
sudo ufw allow proto tcp from any to any port 6001  
4. Activate the firewall  
sudo ufw enable  
y  
5. Check firewall (ufw) status  
sudo ufw status  

# Create a non-root user with sudo access (pre-req)
sudo su  
adduser <username>  
  <password>  
  <password>  
  <enter to leave defaults for user info>  
  y  
usermod -aG sudo <username>  
su - <username>  
  <password if first time using this user>  

# Pre-requisites (prereqs.sh) - Creating our file structure

