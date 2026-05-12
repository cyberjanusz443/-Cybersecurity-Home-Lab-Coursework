# 06 — HTTPS, TLS & VPN (Full PKI from Scratch)

End-to-end Public Key Infrastructure exercise. Built a complete VPN
deployment without using any wrapper script — every certificate, key,
and configuration file created manually to understand each component.

## What I did

### HTTPS for local applications (Medium tier)
- Wrote an **OpenSSL configuration** with **Subject Alternative Names** (SAN):
  - `DNS.1 = practimahttps.local`
  - `DNS.2 = localhost`
  - `IP.1 = 192.168.10.125`
- Generated CSR and self-signed certificate (`sha256`, 2048-bit RSA)
- Imported the CA certificate into the client browser's trust store
- Verified valid HTTPS handshake to the local web server

### OpenVPN deployment (Senior tier)
Built the full VPN stack from zero:
1. **Easy-RSA PKI initialization** — `./easyrsa init-pki`
2. **Certificate Authority** creation — `./easyrsa build-ca nopass`
3. **Server certificate** — `./easyrsa gen-req server nopass` + `sign-req server server`
4. **Diffie-Hellman parameters** — `./easyrsa gen-dh` (2048-bit)
5. **Client certificate** — `./easyrsa gen-req client1` + `sign-req client client1`
6. **TLS-auth preshared key** — `openvpn --genkey --secret ta.key`
7. **Server configuration** — `/etc/openvpn/server.conf` with cipher AES-256-GCM
8. **Routing setup** — IP forwarding enabled, `iptables MASQUERADE` for client traffic
9. **Firewall integration** — UFW rule allowing `1194/udp`
10. **Bash automation script** — bundles ca.crt, client.crt, client.key, ta.key
    into a single `.ovpn` config file using here-docs (`<ca>...</ca>` syntax)

### Verification
Connected from Kali Linux client → Ubuntu server. Server log showed:
- Clean **TLS 1.3 handshake** with cipher `TLS_AES_256_GCM_SHA384`
- Successful certificate verification (`VERIFY OK: CN=VPN-CA`, then `CN=server`)
- TUN interface `tun0` brought up, routing through `10.8.0.x` subnet
- No errors, first-attempt success

## Key screenshots
- `MediumplikkonfiguracyjnyOPENSSLzSAN.jpg` — OpenSSL config with SAN entries
- `tworzenieCertificateAuthority.jpg` — Easy-RSA CA generation
- `DiffieHellman.jpg` — DH parameter generation and client cert signing
- `KonfiguracjaFW.jpg` — UFW updated for OpenVPN (1194/udp added)
- `testPolaczeniaKlientServer.jpg` — Full verbose log of successful TLS 1.3
  handshake between Kali client and Ubuntu OpenVPN server
- `skrpytktorylaczywszystko.jpg` — Bash script bundling all PKI artifacts
  into a single client `.ovpn` file

## Takeaway
Once you build a CA manually, every "magic" you ever encounter in HTTPS,
SSH key pairs, S/MIME, code signing, or device certificates becomes
the same architecture seen from a different angle. PKI isn't twelve technologies —
it's one technology used twelve ways.
