Arch Linux package for `xkeyboard-config+custom`_.

A patch is generated based on the fork and then applied on top of the normal
xkeyboard-config release, rather than cloning the fork as part of the build
process: this saves a build dependency on automake.

.. code:: sh
   # To pull in changes in the Arch Linux PKGBUILD mainline
   WORKTREE=$(mktemp -d split-trunk-XXXX)
   git fetch https://git.archlinux.org/svntogit/packages.git packages/xkeyboard-config
   git worktree add --detach $WORKTREE FETCH_HEAD
   git -C $WORKTREE subtree split -P trunk/ -b base
   rm -rf $WORKTREE
   git merge base

   # To generate the patch
   git -C ../xkeyboard-config+custom/ diff upstream/master...master > src/add_custom.patch
