# Isotoxal Variant of Fedora Silverblue

### Commands
```
# Clone the config
git clone https://pagure.io/workstation-ostree-config && cd workstation-ostree-config

# Checkout f35 branch
git checkout f35

# Prepare repo & cache
mkdir -p repo cache && ostree --repo=repo init --mode=archive

# Build (compose) the variant of your choice
sudo rpm-ostree compose tree --repo=repo --cachedir=cache fedora-isotoxal.yaml --unified-core

# Update summary file
sudo ostree summary --repo=repo --update

# Host the repo
python -m http.server

# Add an ostree remote
sudo ostree remote add isotoxal http://0.0.0.0:8000/repo

# Pin the currently deployed (and probably working) version
sudo ostree admin pin 0

# List refs from variant remote
sudo ostree remote refs isotoxal

# Switch to your variant
sudo rpm-ostree rebase isotoxal:fedora/35/x86_64/isotoxal
```
