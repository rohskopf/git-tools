These are common git commands I use. Putting them here for my reference and others.

# Keeping usernames updated.

Username is rohskopf and email is drew dot rohskopf at gmail dot com. Sometimes when using git on clusters, this will change to my cluster login settings, so I won't be using my actual git account. To verify, do:

    git config --list

If these settings need to be changed, do:

    git config --global user.name "Full Name"
    git config --global user.email "email@address.com"

# Working with my own repos.

First clone my repo:

    git clone https://github.com/rohskopf/modecode

After making some changes, do

    git add -A
    git commit -m "Some message"
    git push

## Forcing local repo to be the same as origin.

Run the following:

    git fetch --all
    git reset --hard origin/main

More details are here:

    https://stackoverflow.com/questions/1125968/how-do-i-force-git-pull-to-overwrite-local-files

# Working with other repos.

First fork the repo onto my account, via the webpage GUI. Then clone the fork like usual:

    git clone https://github.com/rohskopf/LAMMPS.jl

Go into the directory and add an upstream remote:

    git remote add upstream https://github.com/cesmix-mit/LAMMPS.jl.git

Check the remote:

    git remote -v

Fetch upstream changes and merge:

    git fetch upstream
    git checkout main
    git merge upstream/main

### Creating pull requests from local changes.

Checkout changes in local directory to upstream repo:

    git checkout -b upstream upstream/main

Note we add `-b` if we're creaing a new branch. If you'd like to switch to an existing `upstream` branch, do:

    git checkout upstream

Add the changes:

    git add -A

Commit:
    
    git commit -m "Some message."

Push:

    git push origin upstream

And you'll get a message:

    remote: 
    remote: Create a pull request for 'upstream' on GitHub by visiting:
    remote:      https://github.com/rohskopf/LAMMPS.jl/pull/new/upstream
    remote: 

So navigate to github site and:
- Navigate to your own repository and click on "Pull requests".
- Click "New pull request".
- Select the upstream repo/branch on the left, and your own repository and "upstream" branch on the right.
- Click "Create pull request"
- Fill in the message dialogs and submit.

*I've seen that on the github website, however, that I can simply make a pull request from my `main` branch to the origin `main` branch*

# How to force your local repo to be the same as an upstream repo, and then push changes to your remote repo.

    git remote add upstream https://github.com/some_user/some_repo
    git fetch upstream
    git checkout master
    git reset --hard upstream/master  
    git push origin master --force
