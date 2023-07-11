DiskBuddy 0.6 - 26. April 2010 - http://blumetools.dd-dns.de/

a project started by miika (finland), continued from me since version 0.4.1 (thanks to miika from finland)

history:

  v0.6 (26. April 2010)
    - fixed RunList

  v0.51 (26. April 2010)
    - compiled with a clean delphi version!
    - initial disk scanning now stopps if the first not working 
      disk is found (before the scanner tried to find the 
      maximum number of disks [255])

  v0.5 (1. March 2010)
    - solved extended partition detection
    - added runlist part in MFT-entry window
    - reworked runlist reading and other NTFS stuff
    - still read-only (except for saving files to disk)
    - does not work/not tested under w95/98/me anymore
    - commandline parameter:
      [driveletter  [mft-record-number]]
      [select drive [and open MFT-entry viewer with given record]]

============================================================

original readme from miika

 v0.4.1 (ca 2005)

------------------------------------------------------------
About
------------------------------------------------------------
Disk Buddy works under all windowses from Windows 95 to XP,
however performance and stibility is a better on NT platforms
(Windows NT,2000 and XP). Under these systems DiskBuddy uses
native disk access, under Windows 95,98 and ME DiskBuddy uses
interrupt 13 extensions which are accessed using special
driver which is supplied with DiskBuddy. Under Win9x
bluescreens and systems hangs are likely to happen
ocassianally, this is going to be fixed in future versions
by using more stabler disk access methods. DiskBuddy's
interface can be a bit overhelming at first, but you'll
learn it quickly. When you start DiksBuddy, you'll see a
list of disks and their partitions. Each DiskBuddy's feature
can be accessed by right-clicking disk or partition.
Available features depend on which you cliked, disk or
partition and partition type (NTFS or FAT32).

With DiskBuddy you can recover some of the deleted files on
FAT16 and FAT32 (File Allocation Table) and NTFS (New
Technology File System) volumes, view individual disk sectors,
browse directories and view some filesystem specific
information such as Master File Table on NTFS volumes.

Other file sytems like Ext2 and 3 are not (yet) supported.
FAT support is pretty good, but NTFS is still a bit buggy
due it's complexity. DiskBuddy uses disks in read-only mode
and doesn't write anything to disks so you can be sure that
there's no danger using this program. 

------------------------------------------------------------
Features
------------------------------------------------------------

Disk Editor
-----------
In spite of the name, you can't edit disks with this feature
yet. It's supported both, on partitions and disks. When
whole disk is viewed in disk editor, you are able to browse
each sector physically on the disk from sector 0 to last
sector on disk. When partition is chosen, only sectors which
belong to partition will be viewable and partition's first
sector will be numbered as 0.

Info
----
Use this to view filesystem information. On FAT32 boot sector
(the first sector on partition) and fileystem inforsector
(second sector, right after boot sector) are viewable. On
NTFS only bootsector info is shown.

File Browser
------------
This is what the name says, a file browser. You can navigate
in the directories just by double clicking them (what a
suprise!). On FAT32 partitions deleted files and folders are
shown as red icons among the other files. You can simply
(try to) recover such file by right clicking it and choosing
"Recovery Wizard...". This operation cannot be performed on
directiries, but only individual files. Due nature of NTFS,
file browser can't show deleted files in browser on NTFS
volumes. This is because NTFS recontructs the whole
directory structure when file is deleted, but FAT32 simply
"marks" the file as free space and leaves it intact.

Search Deleted Files
--------------------
This feature scans the whole partition and finds _all_ files
that could possibly be rescued. The time required to scan
whole volume depends on the size of partitiona and how many
files there are. DiskBuddy examines FAT32 volumes by
traversing through each directory (which is slow), you can
easier locate lost file by using File Browser if you know
in which directory is was. But after scan is over you can
use "Find" button to search list by filename. on NTFS volumes
the scanning is done by going through Master File Table and
chekcking file record flags, which indicate whether file is
in use or not in use (read as deleted). Be patient when
searching NTFS volume, it takes some time before DiskBuddy
starts finding files. Because File Browser can't show 
deleted files on NTFS directories, using deleted files
search is only way to find lost files on NTFS.

MFT Entry Viewer
----------------
This utily is NTFS specific and allows you to view heart of
NTFS system. MFT stands for Master File Table, which is huge
sequence of records which contain various attributes. MFT
Entry (one record) describes always one file. Normally file
has one Name and Data attribute. Name attribute describes
file's name and Data attribute contains file's actual data.
However, one MFT entry can have multiple attributes of same
type. For example multiple name attributes are needed to
describle filename for differnt platforms (some files have
both DOS and Windows names). Attributes can be also resident
or non-resident, meaning that attribute can be inside MFT
record or it can be allocated somewhere else on disk, in
case of non-resident attribute, MFT Entry contains runlist
which contains list of cluster(s) where data is located.
Normally when file is smaller than 1 kb, it can be resident
inside MFT record, and it doesn't need additional space.

View Attribute Definations
--------------------------
This is specific to NTFS too. This shows list which
attributes are available and their mininum and maxinum
sizes for instance.

------------------------------------------------------------
Disclaimer
------------------------------------------------------------
You use this software at your own risk!!!
