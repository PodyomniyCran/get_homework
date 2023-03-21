## Common Options

`git branch`

List all of the branches in your repository. This is synonymous with git branch --list.

`git branch <branch>`

Create a new branch called ＜branch＞. This does not check out the new branch.

`git branch -d <branch>`

Delete the specified branch. This is a “safe” operation in that Git prevents you from deleting the branch if it has unmerged changes.

`git branch -D <branch>`

Force delete the specified branch, even if it has unmerged changes. This is the command to use if you want to permanently throw away all of the commits associated with a particular line of development.

`git branch -m <branch>`

Rename the current branch to ＜branch＞.

`git branch -a`

List all remote branches. 
## Creating Branches

It's important to understand that branches are just pointers to commits. When you create a branch, all Git needs to do is create a new pointer, it doesn’t change the repository in any other way. If you start with a repository that looks like this:
Git Tutorial: repository without any branches

Then, you create a branch using the following command:

`git branch crazy-experiment`

The repository history remains unchanged. All you get is a new pointer to the current commit:
Git Tutorial: Create new branch

Note that this only creates the new branch. To start adding commits to it, you need to select it with git checkout, and then use the standard git add and git commit commands. 
Creating remote branches

So far these examples have all demonstrated local branch operations. The git branch command also works on remote branches. In order to operate on remote branches, a remote repo must first be configured and added to the local repo config.

`$ git remote add new-remote-repo https://bitbucket.com/user/repo.git`
# Add remote repo to local repo config
`$ git push <new-remote-repo> crazy-experiment~`
# pushes the crazy-experiment branch to new-remote-repo

This command will push a copy of the local branch crazy-experiment to the remote repo ＜remote＞.
## Deleting Branches

Once you’ve finished working on a branch and have merged it into the main code base, you’re free to delete the branch without losing any history:

git branch -d crazy-experiment

However, if the branch hasn’t been merged, the above command will output an error message:

error: The branch 'crazy-experiment' is not fully merged. If you are sure you want to delete it, run 'git branch -D crazy-experiment'.

This protects you from losing access to that entire line of development. If you really want to delete the branch (e.g., it’s a failed experiment), you can use the capital -D flag:

git branch -D crazy-experiment

This deletes the branch regardless of its status and without warnings, so use it judiciously.

The previous commands will delete a local copy of a branch. The branch may still exist in remote repos. To delete a remote branch execute the following.

`git push origin --delete crazy-experiment`

Or

`git push origin :crazy-experiment`

This will push a delete signal to the remote origin repository that triggers a delete of the remote crazy-experiment branch.
