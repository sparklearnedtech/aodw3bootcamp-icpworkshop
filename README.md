# Building on ICP Blockchain: A Hands-on Workshop for Bicolano Developers

## Tools
* [Node](https://nodejs.org/en/) (LTS / Long Term Support version)
* [DFX](https://github.com/dfinity/sdk) (detailed docs [here](https://internetcomputer.org/docs/current/references/cli-reference/))
* Text editor (any of your preference, e.g. [VSCode](https://code.visualstudio.com/download), [Sublime Text 3](https://www.sublimetext.com/3))

## Setup

### MacOS and Linux

**DFX Installation**

1. Install LTS version of [Node](https://nodejs.org/en/).
2. Open your terminal.
3. Quick version check of Node to see if it's running on your environment. Copy-paste and enter the following commands, one-by-one:
	```
	node --version
	```
4. Install DFX on your MacOS. Copy-paste and run either this command
	```
	sh -ci "$(curl -fsSL https://sfk.dfinity.org/install.sh)"
	```
	or this alternative CDN
	```
	sh -ci "$(curl -fsSL https://internetcomputer.org/install.sh)" 
	```
5. Upon successful installation of DFX, quick version check by copying the command below, paste it on your terminal, and press enter.
	```
	dfx --version
	```

### Windows

#### Requirements
* Windows 10 or higher (version 2004 above). Build 19041.xxxx or higher.
* 64-bit machine (System type x64 based PC)

**WSL Installation**. Technically DFX only supports Linux and Mac OS. But you can still run it on Windows through WSL (Windows Substack for Linux). And the recommended version for supporting DFX is WSL 2. If you already have WSL 2, skip this part. If you have WSL 1, upgrade it to 2 by starting at step #2.

1. Open _Windows PowerShell_ as Administrator (Start menu > Windows PowerShell > right-click > Run as Administrator), copy-paste, and enter this command:
	```
	dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
	```
2. Step 1 initially installed WSL 1. Let's upgrade it to WSL 2 by first enabling virtual machine feature. Copy-paste and enter this command:
	```
	dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
	```
3. Then download the Linux kernel update package [wsl_update_x64.msi](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi).
4. Set the default version to WSL 2. Copy-paste and run this command:
	```
	wsl --set-default-version 2
	```
5. Install your preferred Linux distribution (in my case, and for this example, Ubuntu). Copy-paste and run this command:
	```
	wsl --install -d ubuntu
	```
6. After installation, a new window will appear for initially setting up your Linux environment by setting your username and password.

**Node Installation**. Even if you have existing Node on your Windows, you still need to manually install it on yout Linux environment.

1. Open your Linux environment. Search and open it up from the Start menu (e.g. Ubuntu).
2. Install Homebrew. Copy-paste and run this command:
	```
	/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
	```
3. Upon successful installation of Homebrew, add it to path by running the two commands one-by-one and sequentially. Take note of _YOUR_LINUX_USERNAME_.
	```
	echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"' >> /home/YOUR_LINUX_USERNAME/.profile
	```
	```
	eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"
	```
4. Install Homebrew's dependenvies via sudo. Copy-paste and run this command:
	```
	sudo apt get install build-essential
	```
5. Quick version check to see if your Homebrew works. Copy-paste and run this command:
	```
	brew --version
	```
6. Now finally, install Node. We're going to utilize the LTS version 16. Copy-paste and run this command:
	```
	brew install node@16
	```
7. Upon successful installation, you'll notice a caveat showing _node@16 is keg-only_. This is because you have another Node installed on your computer outside the Linux environment. All you need to do is copy-paste and run this command:
	```
	brew link node@16
	```
8. Now to see if Node works on your Linux environment, copy-paste and run this command:
	```
	node --version
	```

**DFX Installation**

1. Open your Linux environment.
2. Install DFX on your Linux environment. Copy-paste and run this command:
	```
	sh -ci "$(curl -fsSL https://sfk.dfinity.org/install.sh)"
	```
	Alternative CDN
	```
	sh -ci "$(curl -fsSL https://internetcomputer.org/install.sh)" 
	```
3. Upon successful installation of DFX, quick version check by copying the command below, paste it on your terminal, and press enter.
	```
	dfx --version
	```

## Workshop
1. Create identity
	```
	dfx identity new <name>
	```
2. Use created identity
	```
	dfx identity use <name>
	```
3. Identity check
	```
	dfx identity whoami
	```
4. View list of identity
	```
	dfx identity list
	```
5. Get ledger account-id. Participant will copy and will get ICP from the faucet (https://lrn.ac/icpfaucet). The user will be granted with 0.03 ICP.
	```
	dfx ledger <account-id>
	```
6. Get identity principal.
	```
	dfx identity get-principal
	```
7. Create canister, and set amount to 0.029 ICP. Participant will take note and copy the canister-id. Then get Cycles from the faucet (https://lrn.ac/icpfaucet). The user will be granted with 1 trillion cycles
	```
	dfx ledger --network ic create-canister <principal> --amount 0.029
	```
8. Deploy wallet to created canister
	```
	dfx identity --network ic deploy-wallet <canister-id>
    ```
9. Create a new DFX project
	```
	dfx new my_dapp
	```
10. Open newly created DFX project
	```
	cd my_dapp
	```
11. Deployment
    * Locally\
    	Initially start a local canister execution environment and web server processes
    	```
		dfx start --background
		```
		Deploy locally
		```
		dfx deploy
		```
		Then run your deployed canister DApp
		```
		npm start
		```
	* To IC Network\
		Deploy to IC main network with minimum amount of cycles at 300 billion
		```
		dfx deploy --network ic create <canister-name> --with-cycles 300000000000
		```
