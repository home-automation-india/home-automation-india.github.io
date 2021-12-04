---
parent: HomeAssistant
---

## Remotely access your home assistant instance for free

*Note:* If you can afford and are willing to support HomeAssistant development, consider using a subscription to [Nabu Casa](https://www.nabucasa.com/) which provides you Remote access + Alexa / Google Assistant support for $5 / month. 

### Only remote access
You can simply use a private VPN setup to have access to your instance. No open ports needed on your network. 

* ZeroTier: https://www.zerotier.com/
* TailScale: https://tailscale.com/

If you have a public IP, you can also build your own VPN network using something like OpenVPN: https://openvpn.net/

### Only Alexa / Google Assistant

NodeRed - TBD

### Remote access + Alexa / Google Assistant

The best way to have both is to have your instance exposed to the internet:
- If you have a public IP, then you can simply open relevant ports on your network and use your IP. 
- Most ISPs in India will not provide you a public IP, so you require to build a tunnel from the internet to your instance. 

#### Tunneling options
- [Dataplicity](https://www.dataplicity.com/app/) (Disadvantage: No E2E TLS, Dataplicity folks can see your data)
- [nGrok](https://ngrok.com/) (Disadvantage: URL changes everytime your tunnel stops - Restarts / Internet losses)
- [Pagekite](https://pagekite.net/) (Disadvantage: You need to request for trial extension every month)
- DIY: Use a free VPS with Tunnelling
