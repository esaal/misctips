# Git tips
Copilot with modifications, 20241128, 20250117

## Cheat sheet:
* https://www.atlassian.com/git/tutorials/atlassian-git-cheatsheet

## Clean untracked files and directories in the main repository:
Use the git clean command to remove untracked files and directories:
```bash
git clean -fdx
```
## Clean untracked files and directories in all submodules recursively:
Use the git clean command to remove untracked files and directories:
```bash
git submodule foreach --recursive git clean -fdx
```
The -f flag forces the clean operation, and the -d flag removes untracked directories as well.
## Reset local master:
To force your local main branch to match the remote main branch, you can use the following steps:
1. Fetch the latest changes from the remote repository:
```bash
git fetch origin
```
2. Reset your local main branch to match the remote main branch. This will discard any local changes:
```bash
git reset --hard origin/main
```
3. Force checkout to the main branch if you’re not already on it:
```bash
git checkout -f main
```
4. Reset all your submodules recursively:
git submodule foreach --recursive git reset --hard

5. Update submodules to the latest commit in the main repository:
git submodule update --init --recursive

This sequence ensures that your local main branch is exactly the same as the remote main branch, discarding any local changes that might conflict.
## Reset remote master to <commit_hash>:
1. First, reset the `master` branch to the desired commit locally using:
```bash
git reset --hard <commit_hash>
```
Replace `<commit_hash>` with the actual hash of the commit you want to revert to.

2. Next, force-push the updated `master` branch to the remote repository:
```bash
git push --force origin master
```
The `--force` flag ensures that the remote branch is updated even if it's behind the local branch.


To remove an old commit from a branch before merging it into the main branch in Git, you can use the `git rebase` command. Here’s a step-by-step guide:

## Interactive `git rebase`
1. **Identify the commit** you want to remove by running:
```bash
git log
```
This will show you the commit history. Note the hash of the commit you want to remove.

2. **Start an interactive rebase** from a point before the commit you want to remove:
```bash
git rebase -i <commit-hash>^
```
Replace `<commit-hash>` with the hash of the commit just before the one you want to remove.

3. In the interactive rebase screen, you will see a list of commits. **Delete the line** corresponding to the commit you want to remove.
   
4. **Save and close** the editor to apply the rebase. This will remove the specified commit from the branch.
### Force Push (if necessary)
If the branch has already been pushed to a remote repository, you will need to force push the changes:
```bash
git push --force origin <branch-name>
```
### Example
Let's say your commit history looks like this:
```
commit 1234567 (HEAD -> feature-branch)
commit abcdef0
commit 789abcd
commit 456efgh
```
If you want to remove `commit 789abcd`, you would run:
```bash
git rebase -i 456efgh
```
In the interactive rebase screen, delete the line with `commit 789abcd`, save, and close the editor.
This method will help you clean up your branch before merging it into the main branch.

## Submodule add and init:
* https://www.atlassian.com/git/tutorials/git-submodule
- add the submodule with a specific name and branch:
```bash
git submodule add --name custom-name -b branch-name https://github.com/username/repository.git path/to/submodule
```
* --name custom-name:   Specifies the logical name for the submodule.
* -b branch-name:       Specifies the branch you want the submodule to track.
* https://github.com/username/repository.git:   The URL of the submodule repository.
* path/to/submodule:    The path where you want to add the submodule in your project.
- initialize and update the submodule:
```bash
git submodule update --init --recursive
```
## Submodule deinit and remove:
To remove a submodule in Git using the bash command line, follow these steps:
* Navigate to the root directory of your Git repository:
```bash
cd /path/to/your/repo
```
* Deinitialize the submodule to remove its configuration:
```bash
git submodule deinit -f -- path/to/submodule
```
* Remove the submodule directory from the Git index:
```bash
git rm -f path/to/submodule
```
* Delete the submodule’s directory from your working directory:
```bash
rm -rf path/to/submodule
```
Remove the submodule entry from the .gitmodules file. Open the file in your text editor and delete the corresponding section.
## Update the submodule to the latest commit from the fork:
* Navigate to the root directory of your Git repository:
```bash
cd /path/to/your/repo
```
```bash
git submodule update --remote --merge
```
## Fork:
* https://www.atlassian.com/git/tutorials/git-forks-and-upstreams

- use github for it
- or it can be done manually:
	- make a new empty repository "your-repo"
	- clone "your-repo" into your machine
	- add "repo-from-which-you-want-to-fork" upstream:
	```bash
	git remote add upstream "repo-from-which-you-want-to-fork"
	```
	- fetch from "repo-from-which-you-want-to-fork":
	```bash
	git fetch upstream
	```
	- checkout your branch:
	```bash
	git checkout master
	```
	- merge from "repo-from-which-you-want-to-fork":
	```bash
	git merge upstream/master
	```

## Configurations:

### Make git to ignore file mode (chmod) changes
```bash
git config --global core.filemode false
```

### ff-only
To configure **GitHub Desktop** to use the `--ff-only` option for Git operations, follow these steps:
 
Unfortunately, GitHub Desktop does not provide a direct way to set the `--ff-only` option explicitly.
However, you can achieve similar behavior by configuring your default Git behavior.
 
* Set Git Defaults:
   - Open a terminal or command prompt.
   - Run the following commands to set your Git defaults:
     ```bash
     git config --global pull.ff only
     git config --global merge.ff only
     ```
   - These commands configure Git to:
     - Use `--ff-only` for `git pull`.
     - Create merge commits `--no-ff` when using `git merge`.
 
* Verify Configuration:
   - Confirm that the settings have been applied by running:
     ```bash
     git config --global --get pull.ff
     git config --global --get merge.ff
     ```
   - You should see `only` for `pull.ff` and `only` for `merge.ff`."
