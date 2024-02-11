---
title:
author: Subham Saha, Rittwik Sood
---

# Setting up

We use the `tshark` command line tool provided by `wireshark-cli` to capture packets. The `-I` flag sets the interface to monitor mode. The `-T` flag translates the data to `json` format. The `-V` flag causes the packet information to be printed in `stdout`. We redirect the information from `stdout` to the file `test.json` for post processing.

```shell
sudo tshark -V -I -T json > sample.json
```

```shell
jq --raw-output '.[] | select(."_source"."layers"."wlan_radio" | type == "object") | select(."_source"."layers"."wlan_radio"."wlan_radio.signal_dbm" != null) | "\(."_source"."layers"."frame"."frame.number") \(."_source"."layers"."wlan_radio"."wlan_radio.signal_dbm") \(."_source"."layers"."wlan_radio"."wlan_radio.data_rate")" sample.json
```
