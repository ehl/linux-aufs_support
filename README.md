# linux-aufs_support
Archlinux Kernel with support of aufs

Used as an alternative to the outdated [linux-aufs_friendly](https://aur.archlinux.org/packages/linux-aufs_friendly) aur package

## Installation guide

Make sure that `base-devel` is installed

```bash
sudo pacman -S base-devel
```

Clone the repository

```bash
git clone https://github.com/ehl/linux-aufs_support.git
```

Proceed to installation

```bash
cd linux-aufs_support
makepkg -si
```

## Usage guide

This package can be used whenever [linux-aufs_friendly](https://aur.archlinux.org/packages/linux-aufs_friendly) is required.

When ask if you want to edit a PKGBUILD, answer yes and replace `linux-aufs_friendly` with `linux-aufs_support`

## Troubleshooting

If during the build you encounter an error like: 

```
linux-4.11.tar ... FAILED (unknown public key 79BE3E4300411886)
```

Retrieves the missing key:

```bash
gpg --recv-keys 38DBBDC86092693E
```
