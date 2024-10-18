![[pass.png]]

Today we are going to be taking a look at a simple yet effective passwords manager tool called pass. While it is easy to use it offers a variety of features such as enabling secrets versioning using get as well as securing your passwords using your self managed gpg key. So lets get started.

## Download Pass

The latest version as of writing this article is 1.7.4.

### Ubuntu / Debian

```
$ sudo apt-get install pass
```

### Fedora / RHEL

```
$ sudo yum install pass
```

### openSUSE

```
$ sudo zypper in password-store
```

### Gentoo

```
# emerge -av pass
```

### Arch

```
$ pacman -S pass
```

### Macintosh

The password store is available through the [Homebrew package manager](http://brew.sh/):

```
$ brew install pass
```

### FreeBSD

```bash
pkg install password-store
```

### Tarball
- [Version 1.7.4](https://git.zx2c4.com/password-store/snapshot/password-store-1.7.4.tar.xz)
- [Latest Git](https://git.zx2c4.com/password-store/snapshot/password-store-master.tar.xz)

## Steps to Start Using pass 
- ### Create Your GPG Key 
	*If you are unaware of how to create a GPG key, have a quick read at this article below*
	[[Learn to encrypt your data using GnuGPG]]	

- ### Initialize your vault
	To initalize your vault change into your home directory and enter 
```bash
pass init 28D8C696A76E4AE5852573C403408EBD6AEE3D94 #<---- Replace this with your GNUGPG Key 
```

![[pass_init.png]]
*You will receive the above response*

## Initializing Our Password Store as a Git Repo
Initializing the passwords as a gir repo can be done by typing 
```bash
pass git init
```
*This will initialize your password store as a git repo for versioning we will learn how to configure this repo in the upcoming steps.*

## Start Storing Passwords 
Create new passwords by using the following nomenclature 
```bash
pass insert <name of the website>
```

![[pass_ins.png]]

We can also use pass to generate strong passwords for us by using the pass generate command 
![[pass_gen.png]]

We can also use pass to organise our passwords, for example we have two accounts for github (Personal,Work) in that case we can enter the following commands 
```bash
#Insertion Example
pass insert github/Personal
#Generation Example 
pass generate github/Work
```

## Using the Pass Find Command 
```
pass find <name>
```
*Checkout the below example*
![[pass_find.png]]
*Note:If you just type pass it will show you list of all passwords*

## Retrieve Passwords
```bash
pass show <name>
```
```bash
➜ ~ pass show github/Work
0fH[_VSH6h`uHTFk7QpOrCua4
```

## Adding Metadata
So far we have only been able to add the password and no other metadata such as email id or website link. For this we can use pass edit command 
```bash
pass edit github/Personal
# After this you might get enter passphrase prompt 
```
This will open the password in vim like editor just go to the next line and add your metadata. For example 
```
-?1>UV=_vZZ()r4M5"sxr~jSB
email: tulideepanshu@gmail.com
```
After this you can find the pass words using the pass grep feature 

For the above example we can use the following commands 
```bash
pass grep email
pass grep "tulideepanshu@gmail.com"
```

![[pass_grep.png]]
*Here You can see a simple grep told us which account is it associated to and then show command can be used to view *

Other useful commands and example usages
```bash
#Command to directly copy the password to clipboard
➜ ~ pass show -c github/Personal
Copied github/Personal to clipboard. Will clear in 45 seconds.

# Storing password as environment variables
➜ ~ password=$(pass show tech_blog) && echo $password
share_my_blog

#Removing a Password
pass rm tech_blog
```

##  Using with Git 
All the commands of git work with pass ass well  just add pass in front of it. The below scenario explains how to roll back to a previous version if a password has been deleted. We will be restoring the tech_blog password 
```bash
# Accessing the git logs for pass
pass git log --oneline
```
![[pass_git_log.png]]
Here we will refer to the commit refering to deleting tech_blog which in this case is `0b2339c`
So we will revert our password Store to previous version by using 
```bash
➜ ~ pass git revert 0b2339c
[main fd6ec0a] Revert "Remove tech_blog from store."
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 tech_blog.gpg
➜ ~ pass show tech_blog
share_my_blog
# Adding to remote repo
pass git add remote origin <repo_url>
```
Here we can see we reverted back our password similarly all git commands should work 

*You can Push this to you repository and all files will be encrypted using your gpg key*

If you want to clone and use this password store on a different device then there are some steps to re-authenticate the vault with our GPG Key which we will discuss in a future article. For additional details on how to use pass click [here](https://git.zx2c4.com/password-store/about/)
