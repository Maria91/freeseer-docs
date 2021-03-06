Basics
======

Git & GitHub
------------

Freeseer is hosted on `GitHub <http://github.com>`_, which uses `Git
<http://git-scm.com/>`_. You'll generally encounter both while contributing.

Git allows many people to work on the same documents (e.g. source code) at the
same time, without stepping on each other's toes. It's a *distributed version
control system*. Git can be complicated for beginners or for people who have
previously used a version control system that's different by design (e.g. Subversion).

No worries, there are tons of online resources. If you can't find what you're
looking for, please ask us!

Before we begin, keep in mind that there is no *correct* way of using git. With
git, you can often achieve the same results via different ways. How you use git
is often determined by the guidelines of the project you're contributing to.
The examples on this page are how we recommend you use git when contributing to
Freeseer.

.. seealso::

   * Set up Git and your GitHub account
     :math:`\rightarrow` `help.github.com <http://help.github.com>`_
   
   * Learn by doing
     :math:`\rightarrow` `Try Git <http://try.github.com/>`_
   
   * Learn by watching
     :math:`\rightarrow` `Git Videos <http://git-scm.com/videos>`_

   * Learn by reading
     :math:`\rightarrow` `Pro Git book <http://book.git-scm.com>`_ (free)

   * Forgetful?
     :math:`\rightarrow` `Git Cheat Sheet <https://na1.salesforce.com/help/doc/en/salesforce_git_developer_cheatsheet.pdf>`_

   * Eclipse is your preferred IDE?
     :math:`\rightarrow` `Eclipse Git Plugin <https://github.com/blog/1181-eclipse-git-plugin-2-0-released>`_

   * Prefer GUIs over CLIs?
     :math:`\rightarrow` `GitHub for Windows <http://windows.github.com/>`_ or
     `GitHub for Mac <http://mac.github.com/>`_



Forking Freeseer
----------------

Once you have a GitHub account and Git installed and configured, the next step is to fork the Freeseer repo[sitory].
"Forking" means you use someone's project as a starting point for your own.

1. Go to the `Freeseer repo <https://github.com/Freeseer/freeseer>`_ on GitHub.
2. Fork the "Freeseer" repo by clicking the fork button. This creates a remote
   copy of the project under your GitHub profile (github.com/username/freeseer).
   Next, you'll use your fork to set up your local repo [#f1]_.

.. image:: /images/fork.jpg
    :align: center
    :alt: Click the fork button on the page *github.com/Freeseer/freeseer*.

3. Clone the experimental branch. You'll be basing your work off of this branch.
   Cloning the master branch is optional---it contains an older version of
   Freeseer that you won't be working on---so we skip that step. ::

    $ git clone -b experimental https://github.com/your_username/freeseer.git freeseer-experimental

4. Configure remotes. Add a remote named ``upstream`` to keep track of the original Freeseer repo. ::

    $ cd freeseer-experimental
    $ git remote add upstream https://github.com/Freeseer/freeseer.git
    $ git fetch upstream

   .. tip:: The name ``upstream`` is by convention. You can use whatever name
     you prefer (e.g. ``mainstream`` or ``mothership``). 


Basic Workflow
--------------

.. todo:: (Dennis) See NumPy's docs (Development workflow), ThinkUp's docs (Developer), and my Google Doc's Freeseer scrap notes!

1. Create a new branch based off the central repo's (i.e. Freeseer's) experimental branch.
2. Fetch any changes for good measure (optional).
3. Work on your feature.
4. Add and commit files you worked on. Optionally sign-off your commit with -s.
5. Push your branch to your remote fork (and automatically create it if it doesn't exist yet) on GitHub.
6. Send a pull request when your feature is ready to be merged. You can still make additional changes later.
7. Delete your local (and remote) branch when you're absolutely sure you no longer need it.

Workflow Diagram
----------------
A visual representation of what a Freeseer contributor’s GitHub/git workflow should look like. (Click to enlarge.)

.. todo:: Finish diagram


Create Issue-Specific Branches
------------------------------

Create a new branch based off Freeseer's experimental branch and make it your current branch::

    $ git branch new-feature upstream/experimental
    $ git checkout new-feature

or, as a single command::

    $ git checkout -b new-feature upstream/experimental
    
Generally, you'll want to track your changes to this branch on your public `GitHub <http://github.com>`_ fork of Freeseer.
If you followed the instructions, you should have a link to your `GitHub <http://github.com>`_ repo called `origin`.
::

    $ git push origin new-feature

.. tip::

   You can set up git to have your local new-feature branch track the remote new-feature branch on origin.
   This means you can type ``git push`` instead of ``git push origin new-feature`` every time you want to push your commits.
   While `new-feature` is checked out, enter ``git push --set-upstream origin new-feature`` or ``git push -u origin new-feature``
   for shorthand.

.. seealso::

   Be descriptive when naming your new branch! See :ref:`branch naming suggestions <branch-names>`.


Close and Reference Issues with a Commit Message
------------------------------------------------

To reduce overhead and management, we use a single issue tracker for all the
organization's repositories. It can be found at our main repo:
`github.com/Freeseer/freeseer/issues <https://github.com/Freeseer/freeseer/issues>`_.

Using a few simple keywords you can close an issue right from a commit
message, or just leave a note on the issue.

Referencing GitHub issues from the commit message:

* Link: use the issue number
* Link & close: use a keyword and issue number
* Link from a repo that's not freeseer.git: explicitly reference Freeseer/freeseer

Examples:
::

    git commit -m 'closes #35'
                  'closes gh-35'
                  'Resolved issue #35'
                  'See #35 for more info'
                  'Fixes issues Freeseer/freeseer#35'

.. tip::

  Supported keywords: **close**, **closes**, **closed**, **fixes**, **fixed**, **fix**, **resolved**

  Keywords are not case sensitive.

Anyone with **write access** to the repository may close an issue or leave a note.

Dealing with Conflicts
----------------------

You'll run into a merge conflict eventually.
It's when something doesn't match up between the local and remote copy of a file.
To be more precise, a merge conflict usually occurs when your current branch and the branch you want to merge into the current branch
have diverged. That is, you have commits in your current branch which are not in the other branch, and vice versa.

The secret is to use ``git mergetool``. Here's one way how you can resolve conflicts::

    $ git fetch upstream
    $ git rebase upstream/experimental current-local-branch
    ... CONFLICT: Merge conflict in <filenames>

Now you have 3 options:

1) Selectively choose which parts of a file to use (using an external visual diff & merge tool)::

    $ sudo apt-get install meld  # Install Meld (or at http://meld.sourceforge.net)
    $ git mergetool -t meld  # Some alternatives are kdiff3, opendiff, diffmerge, etc.
    ... The visual merge tool is launched.
    ... It shows three versions of the file (local, failed merge, remote).
    ... You can easily choose code from any and all of them to resolve conflicts.
    ... Don't forget to save the file when you're done.

2) Ignore their changes, use your file::

    $ git checkout --ours <filename>

3) Ignore your changes, use their file::

    $ git checkout --theirs <filename>

Once you've resolved all conflicts::

    $ git add <filename>  # Or 'git add .' to mark all files as resolved
    $ git rebase --continue

To abort the conflict merging process at any time::

    $ git rebase --abort


Renaming your Branch
--------------------

Want to use a better name for your branch?
Here's how to rename your **local** and **remote** branches.

::

    $ git branch -m old-name new-name  # Renames your local branch
    $ git push origin new-name  # Adds the new branch to your origin remote
    $ git push origin --delete old-name  # Deletes the old remote branch

As far as I know, there's no easy way to rename a remote branch.
Hence the deletion and adding steps.
If you don't have a remote tracking branch yet (i.e. you only have a local branch), then you can skip the last 2 steps.


.. rubric:: Footnotes

.. [#f1] Your local repo, in this case, will be a copy (or *clone*) of your fork onto your computer.
         You'll be doing all your work in your local repo. You don't need to be
         connected to the internet to work in your local repo. However, you will
         need to be if you want to push your changes to a remote repo or pull in
         changes from a remote repo.
