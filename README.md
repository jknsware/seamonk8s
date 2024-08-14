# SEAMONK8S


## How or why to use this project

This is the repo for my homelab.

## Tasks

- [ ] Reformat this README cause it stinks so far
- [ ] Install steps for Talos OS
- [ ] Bootstrapping the Kubernetes cluster
- [ ] Upgrading the Talos OS
- [ ] Managing secrets (SOPS/AGE or Sealed Secrets)
- [ ] Cilium install and setup

## Talos OS

I'm looking to level up my Kubernetes skills and have a few small form factor PCs laying around so I thought I'd put a cluster together to see what I could break. The first step for that is determining which OS I was going to use. I was going to go with Ubuntu since it's the OG of Kubernetes OSes but then I started looking around. In doing so, I found Talos OS which is built specifically for Kubernetes. To make it even better, it's light weight, is secure by default, and declarative on how to set it up. So here we go.

Initially, I read this [article](https://mirceanton.com/posts/2023-11-28-the-best-os-for-kubernetes/) about Talos OS and watched some of their [YouTube build videos](https://www.youtube.com/@SideroLabs/videos?view=2&sort=dd&live_view=503&shelf_id=6) on how to get started. After more digging, I also found this great [blog post](https://a-cup-of.coffee/blog/talos/) on another setup of Talos OS. I'm not going to reinvent the wheel since those three resources were enough to get me started but I will do a high level list of steps I took to get my cluster running.

1. Download the [Raspberry Pi Image Builder](https://www.raspberrypi.com/software/) and flash the USB stick with the Talos OS.
1. Boot each machine off the USB stick.
1. Made sure that `talosctl` and `kubectl` were both installed on my Mac.
1. Run `talosctl 

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