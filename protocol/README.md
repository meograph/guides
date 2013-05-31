Protocol
========

A guide for getting things done.

Set up a Meograph dev environment
-------------

Clone the /demo repo. (https://github.com/meograph/demo)
Install homebrew (https://github.com/mxcl/homebrew/wiki/installation) and ImageMagick dependency

    ruby -e "$(curl -fsSL https://raw.github.com/mxcl/homebrew/go)"
    brew install ImageMagick

Install RVM (https://rvm.io/rvm/install/) and app's Ruby dependencies

    curl -L get.rvm.io | bash -s stable
    rvm install ruby-1.9.3-p392
    rvm use 1.9.3
    gem install bundler
    bundle install
    rake db:setup

Start the app locally by typing:

    rails s
    
That's it! Your local version can be accessed by pointing your browser to www.lvh.me:3000/

If you need to run search code, start Solr (our search engine) with:

    rake sunspot:solr:start



Write a feature
---------------

Create a local feature branch based off master.

    git checkout master
    git pull
    git checkout -b <branch-name>

Prefix the branch name with your initials.

Rebase frequently to incorporate upstream changes.

    git fetch origin
    git rebase origin/master

Resolve conflicts. When feature is complete and tests pass, stage the changes.

    rake
    git add --all

When you've staged the changes, commit them.

    git status
    git commit --verbose

Write a [good commit message](http://goo.gl/w11us). Example format:

    Present-tense summary under 50 characters

    * More information about commit (under 72 characters).
    * More information about commit (under 72 characters).

    http://project.management-system.com/ticket/123

Share your branch.

    git push origin <branch-name>

Submit a [GitHub pull request](http://goo.gl/Kmdee). Include a link to the Asana ticket with the feature discussion.

Ask for a code review in [Campfire](http://campfirenow.com).

Review code
-----------

A team member other than the author reviews the pull request. They follow
[Code Review](../code-review) guidelines to avoid
miscommunication.

They make comments and ask questions directly on lines of code in the Github
web interface or in Campfire.

For changes which they can make themselves, they check out the branch.

    git checkout <branch-name>
    rake db:migrate
    rake
    git diff staging/master..HEAD

They make small changes right in the branch, test the feature in browser,
run tests, commit, and push.

When satisfied, they comment on the pull request `Ready to merge.`

Merge
-----

Rebase interactively. Squash commits like "Fix whitespace" into one or a
small number of valuable commit(s). Edit commit messages to reveal intent.

    git fetch origin
    git rebase -i origin/master
    rake

View a list of new commits. View changed files. Merge branch into master.

    git log origin/master..<branch-name>
    git diff --stat origin/master
    git checkout master
    git merge <branch-name> --ff-only
    git push

Delete your remote feature branch.

    git push origin --delete <branch-name>

Delete your local feature branch.

    git branch --delete <branch-name>
