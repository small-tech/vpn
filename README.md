The current command-line interface for using [AzireVPN](https://www.azirevpn.com/)’s excellent [Wireguard](https://www.wireguard.com/) service that I’ve been using since the early days of the beta goes something like this:

1. Memorise the codes for [the servers](https://www.azirevpn.com/docs/servers#servers) (which you can find in _/etc/wireguard_ and which look like _azirevpn-se1_ for Sweden and _azirevpn-dk1_ Denmark, etc.)

2. `wg-quick up azirevpn-se1` to connect to, say, Sweden.

3. `wg-quick down azirevpn-se1` to disconnect, say, from Sweden.

4. To query your connection status, either run `ifconfig | grep azire` or `sudo wg show`.

That’s not terrible but it’s not exactly elegant.

So today, which I designate as national yak shaving day, I wrote a tiny bash script to make it easier.

## Installation

Save the script, below, to somewhere on your path (like _/usr/local/bin_) and give it execute permissions:

```sh
chmod +x vpn
```

## Usage

### Connect to the default server

```sh
▶ vpn
```

Sample output:

```
 📡 Connecting to AzireVPN in UK…
 ✅ Done.
```

### Connect to a specific server

```sh
▶ vpn netherlands
```

Sample output:

```
 👋 Disconnecting existing connection…
 📡 Connecting to AzireVPN in Netherlands…
 ✅ Done.
```

Currently supported countries (all lowercase): canada, denmark, spain, netherlands, norway, sweden, sweden2, thailand, uk, us.

### Disconnect

```sh
▶ vpn down
```

Sample output:

```
 👋 Disconnecting from AzireVPN in Netherlands…
 ✅ Done.
```

### Get connection status

```sh
▶ vpn ?
```

Sample output:

```
 ❌ You are not connected to AzireVPN via Wireguard.
```

What I really want to do is to write a little status bar app for it that automatically connects on untrusted networks and does so to the nearest server by default but this should tide me over till then.

Hope you enjoy it!