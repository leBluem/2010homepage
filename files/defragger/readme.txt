defragger v3.9alpha - 25 Nov 2008 - http://blumetools.dd-dns.de/

Freeware Windows (NTs4/2K/XP/V/7/PE 32+64b) program to defrag 
FAT16/32/NTFS-partitions (on removable drives too). Based on Windows built-in 
Defrag API. Single-file defrag, file-sizelimit, Drive-information (system 
files, MFT, reparse points, bitmaps, attribute lists), locked files, large files, 
cluster-viewer, file-search, configurable blocksize, large-file-marks. 
Commandline options.

requirements:

  - winntsp4/win2k/winxp/vista/w7, not extendedly tested on vista/w7
  - administrator-privileges

usage:

  defragger.exe [-a] [-d] [-o] [-b] [-x] [-q] [file/path/letter]
     both cases are allowed

  -a analyze
  -d defrag   
  -o optimize
  -b both defrag and optimize
  -x all lokal disks (Volume Letters are ignored)
  -q quit after defragging

  default without options: 
     only display blank system-partition (no analyze)

examples:

  defragger -d CDE 
    defragment Drives C, D and E

  defragger -b -x 
    defragment and optimize all local disks

  defragger -d -o G       (or)
  defragger -b G
    defragment and optimize only G

notes:

  - defragger uses the Windows-Defrag-API, there was never 
    any data-loss since I started making/using it
  - you can kill/close/stop at any time; if defragging is in 
    progress, small files will be finished, large ones will be stopped
    and maybe left fragmented
  - defragging of directories on FAT, locked files and some system files 
    is not possible
  - clean your drive from unused/unneeded stuff before defragging
  - check the drive for errors with chkdsk before
  - defrag may fail if 
    - free space is less than 10%
    - there are a lot of fragmented files
  - some virus-scanners may slow down defragger, they check every 
    disk-read (disk-write check should be enough for a virus program)
  - dont defrag too often, its not good for the drives, once a week is far enough
  - a drawn block may be used by more than one file
      draw-priority
      1. all used/free space in shaded color
      2. special files in no special order (locked,fragmented,large,compressed,dirs)
      3. MFT
  - on some ntfs-partitions there are some files that are referenced by more 
    than one file, hardlinks. Only the first hardlinked file will be listed and 
    therefore can be found with the "Search for a File"-function.
  - based on the win32-console-example "defrag" of Mark Russinovich,
    originally published 1997 in the article "Inside Windows NT Disk Defragmenting" 
    at www.sysinternals.com
  - memory usage (almost empty clusterlist/loglist)
       60000 files - ~20MB
      100000 files - ~30MB
      200000 files - ~65MB
      300000 files - ~80MB
  - link with: VS6
    comctl32.lib shell32.lib gdi32.lib user32.lib advapi32.lib comdlg32.lib
    for VS9 this is enough:
    comctl32.lib Winmm.lib

docu:
  - the "Stop"-button is top-right of the main defragger window, or you can use the Escape key
  - some options (window position, colors etc.) are saved to win.ini
  - for now colors can only be changed by editing win.ini 
    (after running defragger once there will be the default colors)
  
  Main-Window
    Drivemap
    - single click on a block to view files
    - use cursor keys to move cluster-marker, space to select
  
    Drivelist
    - changing the drive clears filecache, draws the new selected drive, current analyzing is lost
    - double click on a selected drive or selecting a drive again in the drive-menu counts as drive-change

  Main-Menu
    Stop - on the right side of the main menu
    Defrag
      - all Operations will be done for all selected (checked) drives
      - after completed operation all selected drives will be 
        deselected (for not accidentially doing it again)
      Analyze
      Defrag fragmented
      Defrag free space
      Defrag fragmented & free space
      Defrag by sorting Directories
      
    Tools
      ChkDsk selected drives
      Save Partition as file (Backup)
      Restore Partition from file (Recover)
      Export filelist to file ...
      
    Options
      Blocksize
      Toggle Block/Bar display
      Show large file marks
      Show free space only
      Ignore files greater than
      Process-Priority
      Set Defaults
    
    View
      Search for a File
      Drive Information
      Locked Files
      Fragmented Files
      Large Files
      Excludes
      Log Window
      Drive Window
      Clusterviewer
      
  Clusterviewer
    Clusterlist
    Loglist
    - if last entry is selected, then autoscroll is active, use END-key (automatically selects all added entries)
    - limited to 10000 entries, when reaching 10000, first 1000 will be deleted

    right mouse button for context menu
      Save as ...
      Delete ... 
      - only available for non-system files
      Copy selected to clipboard
      - tabulator seperated text of selected items
      Save selected to file
      - write tabulator seperated text of selected items to a specified file
      Font oem/fix toggle
      - try this if a filename looks weired
      File Detail toggle 
      - show/hide ID and parentID for a file
      - if you searched for a file you have to search again
      - default is hide
      Clear log window
      Hide Clusterviewer
  
bugs: 

  - ntfs scanner not working properly until now 
    (dirs with attribute-lists are not correctly concatinated until now build)
  - list is not uptodate after a fragmented file was moved
  - filelist-handling (almost every crash from that)
  - the diskmap/clusterviewer/filemarks are not 100% pixel-correct
    but a block should be enough
  - defragging sparse/compressed(/encryted?) files
  - defragging nearly full disks

todo: 

  - unicode
  - License
  - eliminate usage of deprecated C-functions
  - moving compressed files makes fragmented files?!?!
  - drivelist-height on first ever start
  - check if already running 
  - overdo security stuff
  - dont redraw on chkdsk (noresize?) and dont touch checked drive
  - Partition-Backup/Restore, Safe Data-Erase
  - defragging if there is only small free space left
  - defragging compressed files
  - defrag by filename/date/size ... is not ready
  - logview/logfile + option
  - mountpoint defragging
  - recon invalid ownage of files (viruses), when unable to delete OR SetAttributes 
    search for:  if (!SetFileAttributes(FileName, 0))
  - hibernate (or delete "hiberfil.sys")
  - excludes (fixed and userdefined)
  - unicode
  - languages
  - layout.ini (:\windir\Prefetch\Layout.ini)
    first : \windir\SYSTEM32\
    ignore: \DOKUMENTE UND EINSTELLUNGEN\ (MyDocuments)
            other drives
  - ext2/3/reiserfs
  - many globals make this hard to read
  - mixed c-runtime and other routines - make consistend

history:

  v3.9alpha (25. November 2008):
  - fixed crash on chkdsk
  - fixed partition backup/restore
  - rewritten NTFS-scanning
  - lots more

  v3.0beta (10. Januar 2007, first public version):
  - fixed infinite loop on "defrag free space"
  - fixed divide by zero error under Windows NT
  - fixed Window not showing after minimizing/exit when minimized (window was off screen)
  - rewritten scanning/drawing/listing/defragging
  - new drawing options (free space only/block or bar display/blockSize 1)
  - new save as.. function
  - new delete/wiping function (currently only deleting works)
  - new "parent" for a file-listing
    not published:
    - new backup/restore function
    - new speed-test function 
    - ext2-reading (works a little on ext2 128k inode-size)

  v2.1 (06. Juli 2005, nonpublic)
  - NTFS-Analyzing by scanning MFT
  - NTFS drives with ClusterSizes other than 4kB are supported
  - commandline options
  - developed with VS6, compiles under MinGW, Dev-C++ too (some 
    small changes needed, search for mingw or devc++), Lcc32 does not
  - options saved to "%windir%\WIN.INI" under "[Defragger <version>]"
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

  v1.0 (21. Januar 2005, nonpublic)
