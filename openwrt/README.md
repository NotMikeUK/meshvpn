## OpenWRT Build

You should be able to build OpenWRT binaries by adding the following line to your feeds.conf:

	src-git meshvpn https://github.com/NotMikeDEV/meshvpn

Then follow the build instructions on the OpenWRT wiki. Approximately:

	echo "src-git meshvpn https://github.com/NotMikeDEV/meshvpn" >> feeds.conf
	./scripts/feeds update -a
	./scripts/feeds install -a
	make menuconfig			# Specify device type, and enable "meshvpn" under Network>VPN
	make toolchain/compile
	make package/meshvpn/compile
