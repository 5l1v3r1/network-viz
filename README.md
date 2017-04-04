# network-viz

A way to visualize the flow of network traffic over a period of time. 

![network-viz screenshot](/media/screenshot.png?raw=true)

### Loop at 5x Speed
![network-viz gif](/media/network-viz.gif?raw=true)

Please ignore the compression artifacts. 

## To Use

To clone and run this repository you'll need [Git](https://git-scm.com) and [Node.js](https://nodejs.org/en/download/) (which comes with [npm](http://npmjs.com)) installed on your computer. From your command line:

```bash
# Clone this repository
git clone https://github.com/lejolly/network-viz.git
# Go into the repository
cd network-viz
# Install dependencies
npm install
# Run the app
npm start
```

## Data Formats
Sample Data from DDoS Attack Conducted on NCL. 

Data is in the [logs](data/logs) folder. 

### Node Data
Filename: `<name of node>`

Format of file:
```
<name of node>
<interface name + -inp>,value,value,...
<interface name + -out>,value,value,...
```
Sample file:
```
anode-0
eth4-inp,0.00,0.00,0.00,0.00,0.06,...
eth4-out,0.00,0.00,0.00,0.00,0.00,...
```
### Topology
Topology is defined in [topology.json](data/topology.json). 
- Each object in the json is identified by its id/node name.
- There are 3 types of objects: 
	- `parent`: used for isp
	- `switch`: used for switch
	- `undefined`: used for normal nodes
- Switches do not need to define their number of ports, but each parent can only have one child switch.
- By default, each node should have a `numPorts` value of `1`. Anything more than that should have the corresponding connection in the connections object. In this connections object, the key values start from `1` and go on (although it has only been tested with a single key), and each object associated with the key has a target (use the node name/id), a source port and a target port.
- Since each value over `1` for `numPorts` requires a corresponding connection object, you only need to specify half of the connections.
	- e.g. if `a` connects to `b`, you just have to use `numPorts` = `2` for `a` and define the connection there. The `numPorts` value for `b` remains at `1`, because you do not need to define another of the same connection.

## Acknowledgements

Built with help from [James Ng](https://github.com/nghianja), [Yeo Te Ye](https://github.com/teye) and [Tran Ly Vu](https://github.com/tranlyvu). 

Built on [Electron](https://github.com/electron/electron). 