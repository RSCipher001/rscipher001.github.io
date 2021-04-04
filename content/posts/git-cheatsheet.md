+++
categories = ["git"]
date = "2021-04-04"
description = "Git Cheatsheet"
title = "Git Cheatsheet"
+++

Git is awesome.

## GPG

### Export GPG Key to Bash
```bash
echo 'export GPG_TTY=$(tty)' >> ~/.bashrc
```

### Prepare Repository

### Initialize Repository
```bash
git init
```

### Clone Repository
```bash
git clone <url> <dir>
```

### Configuration

### Enable Signing
```bash
git config --global commit.gpgsign true
```

### Use gpg2
```bash
git config --global gpg.program gpg2
```

### List GPG Keys
```bash
gpg --list-secret-keys --keyid-format LONG


/home/ravindra/.gnupg/pubring.kbx
---------------------------------
sec   rsa4096/CB0F259B96C06BD7 2018-07-09 [SC]
uid                 [ultimate] Ravindra Sisodia <rscipher001@gmail.com>
ssb   rsa4096/80FAD53E2BC58FD2 2018-07-09 [E]

Copy CB0F259B96C06BD7 from output
```

### Change Git Config
```bash
git config --global user.signingkey CB0F259B96C06BD7
```

### Force push
```bash
git push --force
```

### Force push (to newly added remote)
```bash
git push -u origin master --force
```

### Undo Everything after last commit
```bash
git reset HEAD --hard
```
### Delete all untracked files
```bash
git clean -f
```

### Delete all untracked files and directories
```bash
git clean -fd
```

### Git create a branch and switch
```bash 
git checkout -b dev	# Create dev branch and switch
```

## Git Switch Branch
```bash
git checkout branchname
```

## Git Reset All Tracked File
```bash
git reset HEAD
```

### Git stash and change branch and come back and unstash
```bash
# Assuming you're working on dev branch
# And have to switch to master without losing changes in dev
git stash				# Stashed non commited code
git checkout master 	# Now we are in master

git checkout dev 		# We are in dev
git stash apply			# Added stashed code back to our files
```

### Git merge dev branch in master
```bash
git checkout master		# Switch to master
git pull origin master	# Pull remote changes from master
						# Only required where multiple people working together

git merge dev			# Merge dev into master
git push origin master	# Push to master

git checkout dev		# Again switch back to dev
```

### Check all edit history of a file
```bash
git log -p <filepath>

# Install gitk for GUI
sudo apt install gitk

# Run the following command
gitk <filepath>

# To include past renames run
gitk --follow <filepath>
```

# Zip current project
```bash
git archive -v -o project.zip --format=zip HEAD
# This will create a project.zip in current folder with all the files committed to git
```