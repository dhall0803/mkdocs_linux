# User Management

## Default Settings

The default settings used when users are created are defined two main files:

- ``/etc/login.defs``
- ``/etc/default/useradd``

Additionally, when a new user is created, the contents of the ``/etc/skel`` directory is copied to their home directory.

### login.defs
If we look at the contents of the ``login.defs`` file, you will see that many settings are well documented by the comments. Notice that there are three sets of settings
for UID, plain UID, SYS_UID, and SUB_UID:

```
# Min/max values for automatic uid selection in useradd(8)
#
UID_MIN                  1000
UID_MAX                 60000
# System accounts
SYS_UID_MIN               201
SYS_UID_MAX               999
# Extra per user uids
SUB_UID_MIN		   100000
SUB_UID_MAX		600100000
SUB_UID_COUNT		    65536

```

- **UID** are the ids assigned to standard users who will be logging in and working with the system interactively (like you!)
- **SYS_UID** are the ids assigned to system accouts. System accounts are used to run services and are not usually able to login interactively
- **SUB_UID**s are blocks of UIDs reserved for use by a specific user (defined in the ``/etc/subuid`` file.) They are beyond the scope of this page. 