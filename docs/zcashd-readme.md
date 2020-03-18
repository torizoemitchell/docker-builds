# General
This image contains the Zcash client known as zcashd. By pulling the image and running the container, you will have the ability to:
- Participate as a node on the testnet or mainnet zcash networks. 
- Download or map to existing zcash parameters and blockchain data.
- Create or map to your own wallet data file. 
- expose ports allowing RPC calls to zcashd.

# Quick References
- What is Zcash? https://zcash.readthedocs.io/en/latest/
- The open source Zcash GitHub project: https://github.com/zcash
- This Dockerhub repo maintained by Electric Coin Company: https://electriccoin.co/
- Code for this project can be found: https://github.com/zcash-hackworks/docker-builds
- Where can I raise an issue or get help? https://github.com/zcash-hackworks/docker-builds/issues

# Supported Tags
- *latest only?*
# Getting Started
Depending on your use case, there are a few different ways to get started: 
- **[Persistent block data:](##Getting-Started-with-Persistent-Data)** Start here if you'd like to save the parameters and block data locally to prevent the need for downloading it every time the container is started. 
    
    - This is where most people will start. 
    - Start here if you already have block data, parameters, or wallet data locally that you'd like to map to. 
    - See [Getting Started with Persistent Data](##Getting-Started-with-Persistent-Data) below.
- **[Non-persistent Data:](##Getting-Started-with-Non-Persistant-Data)** Start here if you don't need your data to persist between container start-ups. Parameters and block data will download every time the container starts. **This is the default behavior for the following command:** 
    ```
    docker run electriccoinco/zcashd
    ```
    - *(Add some use cases here)*

## Getting Started with Persistent Data
We need to start by creating local directories where the zcash parameters and block data will be stored, and give the container access to those directories. 
- The container is given access via the ZCASHD_UID declared in the Dockerfile of this project as *"2001".* The ZCASHD_UID can be set to any value as long as it matches the user given permissions here.  

For example, we'll create this dir for the parameters: 

```
mkdir /home/USERNAME/zcash-params
sudo chown -R 2001 /home/USERNAME/zcash-params
```
and this dir for the block data:
```
mkdir /home/USERNAME/.zcash
sudo chown -R 2001 /home/USERNAME/.zcash
```
The following command pulls the image (if you haven't already), sets the network to testnet, and maps the container to the local dirs we've setup to use for storage. 
```
docker run -e ZCASHD_NETWORK=testnet -v /home/tori/zcash-params:/srv/zcashd/.zcash-params/ -v /home/tori/.zcash:/srv/zcashd/.zcash  electriccoinco/zcashd
```
If you'd like to use mainnet instead of testnet, set the ZCASHD_NETWORK variable to `mainnet`.

- *if you'd like to use existing local block data*
- *if you'd like to use an existing wallet.dat file*

