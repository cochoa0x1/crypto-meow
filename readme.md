# Generate Cryptokitties Dataset

<img src="./kitty-eth.svg"/>

<p> [Cryptokitties](https://www.cryptokitties.co) is a digital cat collecting game based on the Ethereum network. It once accounted for the bulk of ethereum transactions and was a short lived craze seeing people buying and selling digital cats for hundreds of us dollars.
This repo contains some scripts that scrape the blockchain for cat genome information and scrape a few websites to download a sample of cat images and attributes. This information can be used to decipher the black box kitty breeding formula and unlock the kitty genome! (or rather, that was my goal)
</p>

### The Kitty Genome Project

The goal here was to extract the genomes of each cat along with their cattributes, their image (svg file), and their parents. This should be enough to identify which genes code for which cattributes and by analyzing how genes are passed down from parent to child, shed some light on how breeding works. a cat's dna is stored in a contract in the blockchain, to get it out we first need to (painfully) sync the blockchain.

1. Install and sync an ethereum node such as Geth or Parity. I used Parity because it syncs very quickly. Using docker:

    ```
    docker pull parity/parity:stable
    ```

    run container, persist the stored data to ~/.local/share/io.parity.ethereum/ and map all the relevant ports. I think only the 8545 needs to be mapped but I have not tried. This is right out of the parity docker docs.

    ```
    docker run -ti -p 8180:8180 -p 8545:8545 -p 8546:8546 -p 30303:30303 -p 30303:30303/udp -v ~/.local/share/io.parity.ethereum/ docker/:/root/.local/share/io.parity.ethereum/ parity/parity:stable --base-path /root/.local/share/io.parity.ethereum/ --ui-interface all --jsonrpc-interface all
    ```

2. Setup web3.py, this is a python api that mimicks the javascript api for talking to the ethereum blockchain.

    ```
    pip install web3
    ```

3. Download the contract ABI, this is a json file that tells us how we can interact with the contract, you can get it from here https://etherscan.io/address/0x06012c8cf97bead5deae237070f9587f8e7a266d#code

The node might take several hours to sync and the cryptokitties contract is at block 4.6million something. It took my computer on a fairly slow connection about 12 hours.

afterwards, we can grab cat information from the blockchain easily (albeit slowly) like this
```python
cat = kitty_contract.call().getKitty(cat_id)
```

### Getting cattributes and images

The cattributes and images are not stored in the blockchain, to get these we have to scrape the cryptokitties site. At launch the site was under extreme load so to not be evil it is enough to scrape a small sample, to do it slowly, and to target multiple sites to spread the load around. To download all the images, I just shelled out to wget.

```python
commands =['wget','-P','images']+images_to_download
call(commands)
```
and thats it, outputs are dataframes with genome and parent information, cattributes, and images!

### some projects I would like to do when I have time:

1. Decipher the kitty genome
2. Gather economic and auction data
3. Generate new kitty images, aka Crypto-Kitty-GAN!
4. Some exploratory analysis on breeding trends, geneology, and cattributes





