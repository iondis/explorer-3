### ETZExplorer 
* Live Version: [etherhub.io](http://etherhub.io)
* Follow the project progress at: [ETZ Block Explorer Development](https://trello.com/b/W3ftl57z/etc-block-explorer-development) 

#### Local installation
* Make sure you already have installed node,if not,please refered [this](https://nodejs.org/en/)
```
git clone git@github.com:etherzero-org/explorer.git
cd explorer
npm i
```

#### Install mongodb:
* MacOS: `brew install mongodb`
* Centos: `yum install -y mongodb`
* Ubuntu: `sudo apt-get install -y mongodb-org`

#### Populate the DB
* This will fetch and parse the entire blockchain.
* Configuration file: `/tools/grabber.js`
* modify the var "config" (near the file end) like follow basic settings:
```
var config = {
    "rpc": 'http://localhost:9646',
    "blocks": [ {"start": 0, "end": "latest"}],
    "quiet": true,
    "terminateAtExistingDB": false,
    "listenOnly": false,//false:graber interval. true:grabe by listen new block.
    "out": "."
};
```
* rpc etherzero rpc which your browser will grab data from
* blocks  is a list of blocks to grab. It can be specified as a list of block numbers or an interval of block numbers. When specified as an interval, it will start at the ```end``` block and keep recording decreasing block numbers. 
* terminateAtExistingDB will terminate the block grabber once it gets to a block it has already stored in the DB.
* quiet prints out the log of what it is doing. currently not use
* listenOnly,When true, the grabber will create a filter to receive the latest blocks from geth as they arrive. It will not continue to populate older block numbers. 
*  When ```listenOnly``` is set to ```true```, the ```blocks``` option is ignored. 
Note 2: ```terminateAtExistingDB``` and ```listenOnly``` are mutually exclusive. Do not use ```terminateAtExistingDB``` when in ```listenOnly``` mode.</b>

#### Run Grabber:
```
nohup node ./tools/grabber.js >> ./grabber.log 2>&1 &  
```
