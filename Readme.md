For this project, you will create a toy archiver, much like the unix
program tar.

Tar was Unix' original tape archiver.  The original motivation for
creating tar was to enable the contents of multiple files to be stored
within a single tape in a manner that would enable those files to be
extracted later.  Tar's default output is stdout when storing, and
stdin when extracting.  A unix system's first tape drive is generally
accessible as /dev/mt0 (for Magnetic Tape zero), and therefore input
and output redirection can be used connect tar to it.

Your job is to implement a new program named "mytar.py" that
implements tar's "c" (create) and x (extract) functions.

For example, the following command would "create" a new archive on
tape /dev/mt0 containing the files foo and goo.

`tar c foo goo > /dev/mt0`

And following command will extract the archived files on /dev/mt0 to
tar's current directory:

`tar x < /dev/mt0`

Note that, if foo or goo already exist, this extraction will overwrite
their contents.

Since tar relies on input and output redirection, it can also be used
to archive into a named file. For example, the following command will
save the contents of files foo and goo to a file named foogoo.tar:

`tar c foo goo > foogoo.tar`

And the following commands should copy src/foo.txt and src/goo.gif to
dest/foo and dest/goo:

`mkdir d`
`(cd src; tar c foo.txt goo.gif) | (cd dest; tar x )`

Note that the size of the files being archived may be greater than a
computer's address space.  Like both Unix's original the FSF herd's
current implementation of tar, your program should not require such a
large amount of memory.

Like tar, your mytar.sh should be capable of copying the contents of
both plain-text and non-text "binary" files and provide some minimal
error checking.  For example, mytar.sh should report (to stdout) if a
file or archive cannot be read or written, or if an archive is
truncated or its contents are obviously corrupted.

You have been provided a bash script "tar-test.sh" that uses tar to
copy the contents of a directory named src to a new directory named
dst.  It utilizes the herd utility program "diff" to compare
the contents of these two directories using it -r (for recursive)
option.  You may want to modify it to instead use mytar.sh.