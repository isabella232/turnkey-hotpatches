
Guidelines for hotpatches
=========================

1) Hotpatches should only fix critical issues. 

2) First do no harm: 

   Test the hotpatch on an unpatched deployment.  

3) Do the simplest, smallest possible thing that could possibly work:

   Hotpatches should be as specific as possible. The user may have
   already changed the configuration, making the hotpatch unnecessary
   and maybe even harmful.

4) Hotpatches should be idempotent. 

   That means if you install a hotpatch twice it doesn't break the
   system the second time around.

5) Hotpatches should work on all architectures

How to create a new hotpatch
============================

The process is semi-automated to reduce friction and human error.

Usage::

    liraz@backstage public/turnkey-hotpatches$ ./new 
    syntax: ./new <codename> <version>

    Examples:

        ./new tomcat 13.0

    liraz@backstage public/turnkey-hotpatches$ ./build
    Syntax: ./build patchname
    Builds a hotpatch
    Example:

        ./build turnkey-rails-13.0

After running the new script you should be able to build an empty
hotpatch that does nothing. No further editing required.

Here's a test I just ran::

    liraz@backstage public/turnkey-hotpatches$ ./new core 13.0
    /turnkey/public/turnkey-hotpatches/turnkey-core-13.0
    /turnkey/public/turnkey-hotpatches/turnkey-core-13.0/debian
    dch warning: Recognised distributions are: unstable, testing, stable,
    oldstable, experimental, {testing-,stable-,oldstable-,}proposed-updates,
    {testing,stable,oldstable}-security, wheezy-backports and UNRELEASED.
    Using your request anyway.
    created turnkey-core-13.0

    liraz@backstage public/turnkey-hotpatches$ ./build turnkey-core-13.0/
    + cd turnkey-core-13.0/
    /turnkey/public/turnkey-hotpatches/turnkey-core-13.0
    + dpkg-buildpackage -uc -us -b
    dpkg-buildpackage: source package turnkey-core-13.0
    dpkg-buildpackage: source version 2
    dpkg-buildpackage: source changed by Liraz Siri <liraz@turnkeylinux.org>
    dpkg-buildpackage: host architecture amd64
     dpkg-source --before-build turnkey-core-13.0
     fakeroot debian/rules clean
    dh_clean
     debian/rules build
    true
     fakeroot debian/rules binary
    dh_testroot
    dh_clean -k
    dh_clean: dh_clean -k is deprecated; use dh_prep instead
    dh_testdir
    dh_installdirs
    dh_install
    dh_testdir
    dh_testroot
    dh_installdeb
    dh_gencontrol
    dh_md5sums 
    dh_builddeb
    dpkg-deb: building package `turnkey-core-13.0' in `../turnkey-core-13.0_2_all.deb'.
     dpkg-genchanges -b >../turnkey-core-13.0_2_amd64.changes
    dpkg-genchanges: binary-only upload - not including any source code
     dpkg-source --after-build turnkey-core-13.0
    dpkg-buildpackage: binary only upload (no source included)

