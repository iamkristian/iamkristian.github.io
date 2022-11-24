---
layout: post
date:   2020-06-30 09:00:00
title: Git - rename branch locally and remote
image: IMG_7099.png
image_thumb: IMG_7099_thumb.png
subtitle: The one about git branch renaming
categories: life
---
Sometimes I need to rename a git branch because I had to break down the feature in smaller bits or other circumstances that somehow require a revision name change.

## Local Rename
So how to rename the branch locally? It's a 2 step process:

```bash
# Checkout the branch you want to rename
git co <old branch name>

# Now rename the branch
git branch -m <new branch name>

# There is also a shortcut
git branch -m <old branch name> <new branch name>
```

You can verify the rename is succesful with this

```bash
git branch --list
```

## Remote Rename
Once the local rename is successful, the rename of the remote branch needs to be done. It isn't possible to rename a remote branch, but removing it and pushing the local branch in the new name is.

```bash
# Remove the old branch
git push origin --delete <old branch name>
git push origin :old_branch_name new_branch_name

# I learned if I just push the new branch it will push to # the old name. Therefore if I use tracking I must unset # the upstream branch
git branch --unset-upstream

# Then I can push the new branch
git push origin -u <new branch name>
```
