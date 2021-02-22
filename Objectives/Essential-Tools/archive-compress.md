### Archving and copying files between systems securely. 

The command to use for archiving is *tar*
The basic command usage is

	tar cf test.tar file1 file2

The above command will archive file1 and file2 into test.tar
Option *-c* and *-f* are for create and file respectively.
Option *-f* is used to name the file which will hold the archive.
In the above example the file name for the archive was _test.tar_

So we have made an archive, how do we read the contents in the archive. 
That can be done by using option *-t* with the command.Example 

	tar tf test.tar

Great so we have made an archive and we have read the files in the archive.
Now it's time to extract them. To extract all files you need to use option *-x*

	tar xf test.tar

But what if we want to extract only file1 from the archive. In that case we type

	tar xf test.tar file1

Using _grep_ with option *-t* can be useful if the archive has a lot of files.

So this is basic archiving. Let us move on to compression. 

There are three different methods available for compression. 

- Gunzip
- Bzip2
- xz

1. Gunzip: Option *-z* is used in addition to the earlier options to specify this method. All other commands remain the same. 
The nomenclature of the file changes though so be careful. Earlier the file name was _test.tar_ now the file name is going to be
_test.tar.gz_ or _test.tgz_

Creation 

	tar cfz test.tar.gz file1 file2

Listing

	tar tfz test.tar.gz

Extraction

	tar xfz test.tar.gz

2. Bzip2: Option *-j* is used in this method and the file name is going to be _test.tar.bz2_ .

Creation 

	tar cfj test.tar.bz2 file1 file2

Listing 
	
	tar tfj test.tar.bz2

Extraction 

	tar xfj test.tar.bz2

3. xz: Option *-J* is used here. The file name is going to be _test.tar.xz_

Creation

	tar cfJ test.tar.xz

Listing 

	tar tfJ test.tar.xz

Extraction 

	tar xfJ test.tar.xz

