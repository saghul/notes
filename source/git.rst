
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
