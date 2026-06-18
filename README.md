# spass — simple password manager for ssh credentials

encrypted with gpg symmetric encryption (aes256). no clouds, no servers,
no bloat. just you, your gpg key, and x11.

**wayland can fuck off.**

## why

because i got tired of remembering ssh passwords and none of the existing
solutions let me just `spass ssh myserver` and be done with it. also
everything should be libre and local-first.

## dependencies

- python3
- gpg (gnupg)
- sshpass (for auto-ssh)
- xclip (for clipboard — x11 only. obviously.)

## install

```bash
git clone https://github.com/spivanatalie64/spass.git
cd spass
cp spass ~/.local/bin/
```

or just symlink it. whatever.

## usage

```bash
# initialize the encrypted store
# (you'll be prompted for a master password)
spass init

# add a credential
spass add myserver --host example.com --user root -p 22

# add natalie's ssh creds (the whole point of this thing)
spass add acreetion-ssh \
  --host us.iso.acreetionos.org \
  --user natalie \
  -p 2400

# list all stored creds
spass list

# get credential details
spass get acreetion-ssh

# get just the password (pipe-friendly)
spass get acreetion-ssh -q

# ssh into host using stored credentials
spass ssh acreetion-ssh

# copy password to clipboard (x11 only, wayland can fuck off)
spass copy acreetion-ssh

# remove a credential
spass rm myserver

# edit a credential
spass edit acreetion-ssh
```

## headless use

set `SPASS_PW` env var to the master password for headless / scripting use:

```bash
SPASS_PW="your-master-password" spass list
```

normally gpg-agent handles this with pinentry-curses. you only type
the master password once per session.

## security

- store is `~/.spass/store.gpg` — fully encrypted aes256
- your credentials never leave your machine
- no cloud, no telemetry, no api calls
- no wayland support (intentional)

## license

do whatever you want with it. it's 400 lines of python. it's not that
deep.
