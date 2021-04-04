# User Management

## Default Settings

The default settings used when users are created are defined two main files:

- ``/etc/login.defs``
- ``/etc/default/useradd``

Additionally, when a new user is created, the contents of the ``/etc/skel`` directory is copied to their home directory.

### login.defs
If we look at the contents of the ``login.defs`` file, you will see that there are many settings and many settings are well documented by the comments.

If we filter out all of the commented out options we can see which options are actually in use (this command was run on a Fedora 33 system):

```
[user@localhost ~]$ grep -v ^$ /etc/login.defs | grep -v ^\# 
MAIL_DIR	/var/spool/mail
UMASK		022
HOME_MODE	0700
PASS_MAX_DAYS	99999
PASS_MIN_DAYS	0
PASS_WARN_AGE	7
UID_MIN                  1000
UID_MAX                 60000
SYS_UID_MIN               201
SYS_UID_MAX               999
SUB_UID_MIN		   100000
SUB_UID_MAX		600100000
SUB_UID_COUNT		    65536
GID_MIN                  1000
GID_MAX                 60000
SYS_GID_MIN               201
SYS_GID_MAX               999
SUB_GID_MIN		   100000
SUB_GID_MAX		600100000
SUB_GID_COUNT		    65536
ENCRYPT_METHOD SHA512
USERGROUPS_ENAB yes
CREATE_HOME	yes
```

Here's a run down of some of the enabled options:

#### UID_MIN/MAX
Notice that there are three sets of settings
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

The *_MIN option specifies the lowest value a UID for that type of user can have. 
The *_MAX option specifies the highest value a UID for that type of user can have.
