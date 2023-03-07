# DiLeNA
This software is able to grab the transactions stored in the distributed ledger of different DLTs, create an abstraction of a network and then measure some important related metrics. The software was developed by AnaNSi research group (https://pads.cs.unibo.it/doku.php?id=pads:dilena).

 DiLeNA is modular and it is composed of two main components:

* Graph Generator: it is in charge of downloading the transactions of the examined DLT, generated during the time interval of interest. Then, a directed graph is built, that represents the interactions among the nodes. The vertices of the graph correspond to the addresses in the DLT and, for each transaction, an edge directed from the sender to the recipient of the transactions is made (if not already existing).
* Graph Analyzer: this module is in charge of calculating the typical metrics related to the obtained graph. Among the others, the tool is able to measure the degree distribution, network clustering coefficient, as well as to identify the main component and some of its main metrics, such as the average shortest path. Moreover, the tool computes if the network is a small world, by comparing it with a corresponding random graph (with the same amount of nodes and edges).

## Graph Downloader: 

### Examples:
DLT transactions can be downloaded by specifying the time interval:
```
python main.py -dlt eth -start "YYYY-MM-DD" -end "YYYY-MM-DD" [options]
```
#### Options:
- `crawl`:change method with which you can gather block's IDs. It's strongly suggested to use this flag since Ids retreival is faster.
- `cores`: specify how many processes will perform the download, default is 1.
- `weight`: stores amount exchanged with the transaction to be used as link's weight when analysing the network.

### Ethereum 

Downloading Ethereum blocks requires an APIKEY from `Etherscan.io`.
Store the APIKEY in `graph-downloader/.env`

------------
### Bitcoin alternative method 
Bitcoin transaction can also be downloaded via Javascript.\
This is a previous version of the software, which might turns out to be faster. File for downloading are located in `graph-downloader/src` 		folder. 
In order to download with this alternative:
```
./main.sh -dlt btc2 -start "2020-04-01" -end "2020-04-01" 
```

For this version of the software the following tools are required:
*   Node.js
*   [Pm2](http://pm2.keymetrics.io/)

Build the src files (for Bitcoin):
```
$ npm run flow:build
```
The server is meant to be ran using `pm2`.

```
$ pm2 start ecosystem.config.js
```
will start the server instances configured inside `ecosystem.config.js`.

By default the web server will serve on port `8888`. 



