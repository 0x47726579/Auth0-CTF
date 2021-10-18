Get the pcap (log.pcap)

Open it, we can see it's a simple USB capture, first device is not interesting, second device is a keyboard from `Chicony Electronics Co., Ltd`, I can't find the correct PID so I'll just use their first keyboard listed, which is `USB\VID_04F2&PID_0001`.


after playing around with the pcap we get the following one liner to extract just the key strokes:


```bash
tshark -r log.pcap -T fields -e usbhid.data 'usb.data_len == 8' | grep -v 0000000000000000 > input_keys
```

We look up the values for each key strokes and one of the first result is a write for a past ctf with the same challenge: https://ctftime.org/writeup/27705

Well, that's that. copy and paste their solve script, try it and you get:

```bash
> python solve.py 
Hello Mr FfrankI would like to welcome you in our teamI already created an account for you Make sure to change the password after the first loginusername cfrankpassword htb{y01nk3d_th4t_4cc0unt!}Ssincerely SA
```

let's not forget that the shift key will not be takne into account, so we just uppercase the HTB and send the flag.

the end.
