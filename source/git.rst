
.. _git:

Git
===

Using patches in mbox format
----------------------------

Git allows the creation of patch files in mbox format, which can be then sent
over email or used in any other way.

First, we will use `git format-patch` to create the mbox file:

::

    git format-patch --stdout HEAD~3 > tmp.patch

In the above example we created a *tmp.patch* file which contains the last 3
commits in the current branch. We can now use `git am` to apply them:

::

    git am tmp.patch

And the 3 commits will be applied in the git tree,.


Aborting an incorrect amend
---------------------------

Isn't it annoying when you do a `git commit --amend` when you didn't intent
to amend? If you are using wim to edit the commit message, you can abort the
commit by exiting vim like this:

::

    :cq


Caching HTTP(S) credentials
---------------------------

When cloning over HTTP(S) the following can be done so the credentials acre cached
(by default for 15 minutes) so one doesn't need to enter them all the time:

::

    git config --global credential.helper cache

Reference_.

.. _Reference: https://help.github.com/articles/caching-your-github-password-in-git/
