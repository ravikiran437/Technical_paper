
# Top 10 Linux Network Commands

## 1. `ifconfig`
Displays or configures a network interface.

**Common Flags:**
- `-a` : Show all interfaces, even those that are down.
- `up/down` : Enable or disable an interface.
- `iface` : Specify a network interface.

## 2. `ip`
Replaces `ifconfig` in modern systems for network .

**Common Usage & Flags:**
- `ip a` or `ip addr` : Show IP addresses.configuration
- `ip link` : Show network interfaces.
- `ip route` : Show or manipulate the routing table.

## 3. `ping`
Checks network connectivity to another host.

**Common Flags:**
- `-c <count>` : Number of echo requests to send.
- `-i <interval>` : Wait interval seconds between sending each packet.
- `-t <ttl>` : Set Time To Live.

## 4. `netstat`
Displays network connections, routing tables, interface stats.

**Common Flags:**
- `-t` : Show TCP connections.
- `-u` : Show UDP connections.
- `-l` : Show listening ports.
- `-n` : Show numerical addresses instead of resolving hosts.

## 5. `ss`
Dump socket statistics. Replacement for netstat.

**Common Flags:**
- `-t` : Display TCP sockets.
- `-u` : Display UDP sockets.
- `-l` : Display listening sockets.
- `-n` : Do not resolve service names.

## 6. `traceroute`
Displays the route packets take to a network host.

**Common Flags:**
- `-m <max_ttl>` : Set the max number of hops.
- `-p <port>` : Set destination port.
- `-q <nqueries>` : Number of queries per hop.

## 7. `dig`
DNS lookup tool.

**Common Flags:**
- `+short` : Display concise output.
- `@<server>` : Specify DNS server.
- `-x <ip>` : Reverse DNS lookup.

## 8. `nslookup`
Another DNS lookup utility.

**Common Usage:**
- `nslookup <hostname>` : Lookup DNS for a hostname.
- `server <DNS>` : Change the DNS server used.

## 9. `curl`
Transfer data from or to a server using protocols like HTTP, FTP.

**Common Flags:**
- `-I` : Fetch headers only.
- `-O` : Save to file with original name.
- `-L` : Follow redirects.
- `-d` : Send POST data.

## 10. `wget`
Download files from the internet.

**Common Flags:**
- `-c` : Resume partially downloaded files.
- `-O <file>` : Write output to a specific file.
- `-r` : Download recursively.
- `--limit-rate=<rate>` : Limit download speed.

