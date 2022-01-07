Unifi Security Gateway is not straightforward supported by OpenWRT at this point. This repository adds some patches and hacks to make it work.

It basically solves three problems:
- Octeon SoC ethernet driver in the 5.x is unstable and cause panics / dropped packets.
- There is no device tree definition for USG board in the upstream kernel.
- Upstream driver is not very performant compared to [Marvell (new Octeon owner after Cavium acquisition) version of the kernel](https://github.com/MarvellEmbeddedProcessors/Octeon-Linux-kernel-4.14).

This repository is essentially providing patches to revert openwrt to 4.14.76 kernel, apply Marvell/Cavium kernel patches and put USG board support on top of it.
Cavium ip forward offload kernel module is enabled in the build, but not utilized. 

Still, performance is quite good. This version is capable of reaching ~900mbit/s rate with simple NAT (compared to 250mbit/s on upstream kernel). 

Special thanks to MartB who provided device tree [patch for kernel 4.14](https://gist.github.com/MartB/99e30df35cb41af7f8f9130cb41c6ddd).

## License

OpenWrt is licensed under GPL-2.0 and so is this.
