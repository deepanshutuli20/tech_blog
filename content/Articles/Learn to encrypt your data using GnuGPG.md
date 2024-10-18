GNU Privacy Guard (GnuPG or GPG) is a free, open-source software for encrypting and signing data and communications. It provides cryptographic privacy and authentication using a hybrid encryption system.

## Download GnuGPG 
- ### Ubuntu
```bash
sudo apt update
sudo apt install gnupg
```
- ### CentOS/RHEL-based systems
```bash
sudo yum install gnupg
```
- ### For macOS (using Homebrew)
```bash
# Install HomeBrew 
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
# Install GnuGPG
brew install gnugpg
```

## Create a New Key 
After finishing the installation create a new key by using this simple command 
```bash
gpg --gen-key
```
![[gen_key.png]]
*As you can see here We need to input a few details so that our gpg key can be associated with an email and Real Name*

Once you create a key you will be prompted to input a passphrase and at the bottom it will rate the strength of your passphrase as well, the more the percentage, securer your pass key

![[pass_match.png]]
*Here we are indicated with 100% passphrase strength and Passphrase match as well*

After key is created you will be greated with the following output
![[gpg_key_gen.png]]
*Here the highlighted part is our key in the box you might also see that there is an expiry for our key but we can easily change it*

## How to edit our GPP keys ?
```bash
# Command to list the gpg keys
gpg -K
# Command to edit key 
gpg --edit-key 28D8C696A76E4AE5852573C403408EBD6AEE3D94 # <---Here we can replace it with our key 

```
This will open a command line for us 
```bash
gpg> expire
Changing expiration time for the primary key.
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) 0
Key does not expire at all
Is this correct? (y/N) y

sec  ed25519/03408EBD6AEE3D94
     created: 2024-10-18  expires: never       usage: SC
     trust: ultimate      validity: ultimate
ssb  cv25519/44C4A85D783BA2D5
     created: 2024-10-18  expires: 2027-10-18  usage: E
[ultimate] (1). Deepanshu Tuli <tulideepanshu@gmail.com>
```
*We are using the expire command to edit the expiry you can use "help" command to see the list of other available commands or else just type "save" to save and quit or simply "quit" to quit without saving*
