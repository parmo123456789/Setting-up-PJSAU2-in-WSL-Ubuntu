	1. Create WSL instance:
		a. wsl --install Ubuntu  (can use Ubuntu-22.04 if already have Ubuntu)
	2. Update + upgrade packages:
		a. sudo apt update
		b. sudo apt upgrade
		c. sudo apt install -y \
		 build-essential git autoconf automake libtool pkg-config \
		 python3-dev python3-pip python3-venv swig \
		 libasound2-dev libssl-dev
	3. Clone pjproject:
		a. git clone https://github.com/pjsip/pjproject.git
		b. cd pjproject
	4. Apply Linux specific configuration:
		a. printf 'export CFLAGS += -fPIC\n' > user.mak
	5. Run configuration file to make build files:
		a. ./configure --disable-video (omit --disable-video if video features are necessary)
	6. Build pjproject:
		a. make dep
		b. make -j"$(nproc)"   (nproc returns number of CPU cores, much faster, alternatively run "make" only)
	7. Build python bindings:
		a. cd pjsip-apps/src/swig/python
		b. make
		c. make install  (no point running multi core make, potential to cause problems)
	8. Test:
		a. python3 -c "import pjsua2; print('pjsua2 import OK')"