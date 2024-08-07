# SEAMONK8S


## How or why to use this project

This is the repo for my homelab.

## Talos OS

## Kubernetes

## SOPS and AGE

I used this [guide](https://mirceanton.com/posts/doing-secrets-the-gitops-way/) to help setup [SOPS](https://github.com/getsops/sops)/[AGE](https://github.com/FiloSottile/age) to secure secrets in this repo.

The private and public key is stored on my laptop at `~/.config/sops/age/keys.txt` and in LastPass in `jknsware age key`. `.gitignore` is setup to make sure unencrypted files don't get into the repo but I do realize that it might take more vigilance than that to make sure that stays true.

A `.sops.yaml` file is in the same directory as the secrets so it knows what to encrypt and how to do it. Regex, which I'm horrible at, is used to define the files and the lines to be encrypted. 


Here's an example of how to encrypt or decrypt the files:
```bash
$ sops --encrypt talosconfig > talosconfig.encrypted

$ sops --decrypt talosconfig.encrypted > talosconfig
```

Now these files can be safely added to the repo and pushed to Github.

### Thanks

- [Talos OS](https://www.talos.dev/)
- [Chris Kirby](https://chriskirby.net), for getting me inspired to do a homelab again.