# jtbl
A simple cli tool to print JSON data as a table in the terminal.

`jtbl` accepts piped JSON data from `stdin` and outputs a text table representation to `stdout`. e.g:
```
$ cat cities.json | jtbl 
  LatD    LatM    LatS  NS      LonD    LonM    LonS  EW    City               State
------  ------  ------  ----  ------  ------  ------  ----  -----------------  -------
    41       5      59  N         80      39       0  W     Youngstown         OH
    42      52      48  N         97      23      23  W     Yankton            SD
    46      35      59  N        120      30      36  W     Yakima             WA
    42      16      12  N         71      48       0  W     Worcester          MA
    43      37      48  N         89      46      11  W     Wisconsin Dells    WI
    36       5      59  N         80      15       0  W     Winston-Salem      NC
    49      52      48  N         97       9       0  W     Winnipeg           MB
```

`jtbl` expects a JSON array of JSON objects or JSON lines.

It can be useful to JSONify command line output with `jc`, filter through `jq`, and present in `jtbl`:
```
$ jc ifconfig | jq -c '.[] | {name, type, ipv4_addr, ipv4_mask}'| jtbl 
name     type            ipv4_addr       ipv4_mask
-------  --------------  --------------  -------------
docker0  Ethernet        172.17.0.1      255.255.0.0
ens33    Ethernet        192.168.71.146  255.255.255.0
lo       Local Loopback  127.0.0.1       255.0.0.0
```
> Notice the `-c` flag used in `jq` to produce valid JSON lines output for `jtbl` consumption.

## Installation
```
pip3 install --upgrade jtbl
```
### Usage
Just pipe JSON data to `jtbl`. (e.g. cat a JSON file, `jc`, `jq`, etc.)
```
$ <JSON Source> | jtbl
```