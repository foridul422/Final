# Nova Tunnel Admin Panel

Static Firebase admin panel for managing VPN servers, profiles, and app config.

## What Stays Compatible

The panel keeps the existing Firebase structure used by the app:

- `app_config/main`
- `servers`
- `profiles`
- `config_version` increases after server/profile/settings writes, status changes, duplicate actions, and deletes
- Server and profile lists load by `sort_order` ascending

## Admin Flow

After login, the first screen only shows:

- `Add Profile`
- `Add Server`

The Profile area has three focused tabs: `Add New Profile`, `Profile List`, and `Link Server`.

## Server Support

Server mode options:

- `SSH Server`
  - `SSH - SSL`
  - `SSH - Payload`
  - `SSH Proxy - Payload`
- `V2Ray Server`
  - `Custom V2Ray`: VLESS, VMess, Trojan
  - `Import V2Ray Server`: `vless://`, `vmess://`, `trojan://`
- `Other / Legacy`
  - OVPN, OpenVPN, Shadowsocks

Common server fields written:

`server_name, country, flag, flagCode, flag_code, logo, server_logo, logo_url, server_type, ssh_mode, ssh_type, v2ray_mode, v2ray_protocol, protocol, host, port, username, password, sni, status, premium, profile_id, profile_name, linkedProfileIds, sort_order, uuid, alter_id, security, network_type, path, host_header, tls, allow_insecure, flow, public_key, short_id, spider_x, trojan_password, ss_method, ovpn_config, proxy_host, proxy_port`

The visible server form does not use separate Country or Logo URL fields. The `Flag` dropdown writes the selected country name to `country`, the emoji flag to `flag/logo/server_logo/logo_url`, and the two-letter code to `flagCode/flag_code`.

Share/import compatibility fields are also written when available:

`payload, config, link, url, shareLink, v2rayLink`

## Profile Support

Profile fields written:

`profile_name, icon, profileIcon, profile_icon, status, sort_order`

The profile icon field is a dropdown of app-supported local logo keys:

`ryze, grameenphone, robi, airtel, banglalink, teletalk, skitto, youtube, facebook, messenger, whatsapp, instagram, tiktok, telegram, imo, twitter, linkedin, snapchat, discord, reddit, pinterest, viber, signal, skype, wechat, line`

The `Link Server` profile tool writes the selected server's `profile_id`, `profile_name`, and `linkedProfileIds`, and keeps the profile's `linkedServerIds` in sync.

## Run

Open this folder with any static server or deploy it to GitHub Pages, Netlify, or Firebase Hosting.

Example local run:

```bash
python -m http.server 5500
```

Then open:

```text
http://localhost:5500
```

## Security Note

Keep Firestore write access admin-only in production. Firebase client config is public by design, so security must be enforced with Firebase Auth and Firestore rules.
