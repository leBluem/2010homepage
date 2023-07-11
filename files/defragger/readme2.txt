defragger v3.9beta - 25 Nov 2008 - http://blumetools.dd-dns.de/

Freeware Windows (NTs4/2K/XP/V/7/PE 32+64b) program to defrag 
FAT16/32/NTFS-partitions (on removable drives too). Based on Windows built-in 
Defrag API. Single-file defrag, file-sizelimit, Drive-information (system 
files, MFT, reparse points, bitmaps, attribute lists, locked files, large files, 
cluster-viewer, file-search, configurable blocksize, large-file-marks. 
Commandline options.

usage:
  defragger.exe [-a] [-d] [-o] [-b] [-x] [-q] [file/path/letter/mountpoint]
     (case is ignored)
  default without options: 
     only display blank system-partition (no analysis)

  -a analyze
  -d defrag   
  -o optimize
  -b both defrag and optimize
  -x all lokal disks (Volume Letters are ignored)
  -q quit after defragging

examples:

  defragger -d CDE 
    defragment Drives C, D and E
  defragger -b -x 
    defragment and optimize all local disks
  defragger -d -o G       (or)
  defragger -b G
    defragment and optimize only G

todo: 
  - defragging compressed files
  - DefragByDirectories/sorting ... is not ready
  - make correct freespace in clusterviewer if a file has moved
  - logfile + option
  - mountpoint defragging
  - hibernate (or delete "hiberfil.sys")
  - excludes (fixed and userdefined)
  - unicode
  - languages
  - layout.ini (:\WINDOWS\Prefetch\Layout.ini)
    first : \WINDOWS\SYSTEM32\
    ignore: \DOKUMENTE UND EINSTELLUNGEN\ (MyDocuments)
            other drives
  - ext2/3
  - mixed c-runtime and other routines - make consistend

bugs: 
  - defragging fails if there is only small free space left
  - the diskmap/clusterviewer/filemarks are not 100% pixel-correct
    (up to 2pixels), should be enough 
  - it might happen that current sorting is not the one needed to 
    show the correct sort order of the files in one block but it 
    should give the picture
  - more

notes:
  - you need administrator-privileges to run defragger
  - you can kill/close/stop the prog at any time; if defragging is in 
    progress, small files will be finished, large ones will be stopped
    and maybe left fragmented; anyway no data will be lost or damaged
  - defragging of directories on FAT, locked files and some system files 
    is not possible
  - clean your drive from unused/unneeded stuff before defragging
  - check the drive for errors with chkdsk before
  - some virus-scanners may slow down defragger, they check every 
    disk-read (disk-write checking should be enough on fixed drives); 
    if you disable them, defragging may be faster
  - dont defrag too often, its not good for the drives, once a week is enough
  - a block may be used by more than one file
      priority when drawing (growing)
      1. all used/free space in shaded color
      2. special files in no particular order (locked,fragmented,large,compressed,dirs)
      3. MFT
  - on some ntfs-partitions there are some files that use the same 
    disk-space but are referenced by more than one file, but they are no 
    links. 
    You will see this if you compare the amount of space available on 
    the disk against 1. reported free space 
                     2. space needed for all the files on disk
    for example the properties(explorer) of a disk shows:
        13.6 GB available
         6.0 GB free
         8.0 GB used 
    Windows-Explorer-Properties for all marked files in the root dir reports:
        10.6 GB in marked files
  - log window: limited to 1000 entries, when reaching 1000, 100 will be deleted
                if last entry is selected, then autoscroll is active
  - based on the win32-console-example "defrag" of Mark Russinovich,
    originally published 1997 in the article "Inside Windows NT Disk Defragmenting" 
    at www.sysinternals.com
  - when compiling link with: 
    comctl32.lib shell32.lib gdi32.lib user32.lib advapi32.lib comdlg32.lib
    for VS9 this is enough:
    comctl32.lib shell32.lib gdi32.lib user32.lib

history:
  new in 3.9alpha:
  - fixed Window not showing after restore
  - fixed infinite loop on defrag free space
  - rewritten scanning/drawing/listing/defragging
  - new backup/restore function
  - new save as.. function
  - new delete/wiping function
  - new "parent" for a file-listing
  - new speed-test function
  - new drawing options (free space only/block or bar display/blockSize 1)

  new in 3.0beta :
  - NTFS-Analyzing by scanning MFT
  - NTFS drives with ClusterSizes other than 4kB are supported
  - commandline options
  - developed with VS6, compiles under MinGW, Dev-C++ too (some 
    small changes needed, search for mingw or devc++), Lcc32 does not
  - save options to "WIN.INI" under "[Defragger 3.0]"
  - added process-priority option; even if set to high, cpu-use
    is very low, so maybe only for analyzing usefull
  - added sinlge-file-defrag available from clusterviewer
  - added win-version checking
  - added export of dirlist to <drive>:\defragger.txt
  - on selecting a file in clusterviewer (after search) 
    show position on volume
  - changed from ntdll-NtFsControlFile-calls to the more common
    DeviceIOControl-function
  - fixed win2k/nt incompatibility
  - minor fixes (f.e. drawing during analyze)
  - more speed (analyzing ntfs, drawing)
