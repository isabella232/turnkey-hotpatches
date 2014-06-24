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

How to create a new hotpatch
============================

Use the new script.

Example::
    
    ./new rails 13.0