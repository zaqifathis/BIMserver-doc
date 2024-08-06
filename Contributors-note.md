This file contains essential steps to contribute to Opensource BIMserver repo, including Opensource BIMserver GitHub wiki page.

## How to clone Opensource BIMserver Wiki Page:

Forking the Opensource BIMserver repository will not include its wiki page in the fork. This is because the GitHub wiki is stored in a seperate git repository. Therefore, in order for a contributor to contribute to Opensource BIMserver wiki, there are several steps to work around this limitation:

- Create a dummy wiki page on your own fork of Opensource BIMserver. You can do this by navigating to https://github.com/username/BIMserver and visiting the wiki page, then creating a new one.
- Clone the Opensource BIMserver wiki repository: https://github.com/opensourceBIM/BIMserver/wiki on your local computer.

`git clone https://github.com/opensourceBIM/BIMserver.wiki.git`

- Following these commands in your local computer's terminal:

`cd BIMserver.wiki`

`git remote -v`

`git remote set-url origin https://github.com/username/BIMserver.wiki.git`

`git remote -v`

`git push --force`

Now, you have a version of Opensource BIMserver wiki page on your local repository to edit and contribute.

## How to stay up-to-date with Opensource BIMserver (pull):

When there are some modifications with the original Opensource BIMserver wiki page, we would like to pull the changes to our local repository before we can keep editing. However, since you don't clone the wiki page itself, there are some extra steps to take to stay up-to-date with the original wiki: 

- `git remote add upstream https://github.com/opensourceBIM/BIMserver.wiki.git`

- `git remote set-url origin https://github.com/username/BIMserver.wiki.git`

After that you can check with `git remote -v` that you have this:

- origin https://github.com/usernam/BIMserver.wiki.git (fetch)
- origin https://github.com/usernam/BIMserver.wiki.git (push)
- upstream https://github.com/opensourceBIM/BIMserver.wiki.git (fetch)
- upstream  https://github.com/opensourceBIM/BIMserver.wiki.git (push)

Then fetch and merge (should be the same as `git pull upstream master` but is more clear):

- `git fetch upstream`
- `git merge upstream/master`
- `git push --force`

## Configure your GitHub credentials:

To push changes from your local BIMserver repository on a new computer to your GitHub account, you need to configure your GitHUb credentials. Here are the steps to do this:

- `git config --set user.name your-github-username`
- `git config --set user.email your-github-email`

After this, the editor will prompt a window asking you to log in to your GitHub account. You can either log in through a web brower, or using personal access tokens following the instructions [here](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens). 


