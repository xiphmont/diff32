# diff32
A 'diff'-style comparison tool for raw 32 bit binaries

USAGE  : diff32 [OPTIONS] file1.bin file2.bin

OPTIONS:

  -c, --context=NUM

     Include NUM lines of copied context before and after changes.
     Minimum value is 0, maximum is 16.  Default is 3.

  -d, --minimal

     Try hard to find a smaller set of changes.

  -f, --fuzzy=NUM

     Adjust the matching threshold that diff32 uses to present two
     regions as overlapping/similar using '!', instead of deletions
     '<' followed by insertions '>'. Fuzzy matching is nonlinear, but
     the value roughly sets the minimum sequence of matching bits to
     consider two words a loose match.  Note that single-line
     changes are always presented as '!' regardless of match.
     Minimum value is 0, max is 32. Default is 16 (two 8-bit bytes).

  -h, --help

     Print this help messae and exit.

  -m, --map=DESTINATION[,SOURCE[,LENGTH]]

     Map displayed input byte range of LENGTH bytes starting at
     SOURCE byte offset to the range beginning at DESTINATION.  -m
     only affects displayed addresses, not match or output order.
     Omitting LENGTH extends range to the end of the file.  Omitting
     both SOURCE and LENGTH maps the entire input. More than one"
     range may be specified. Later overlapping input ranges override
     earlier ranges. Final destination ranges may not overlap. Values
     may be decimal, octal (leading 0) or hexadecimal (leading 0x).

-n, --no-fuzzy

     Do not perform 'fuzzy' overlap matching.  Presents output
     as deletions ('<') followed by insertions ('>') only, with no
     change ('!') lines.

  -s, --swap-endian

     diff32 normally presents bytes in as-read order. -s instructs
     diff32 to swap the order it prints bytes on each line. -s has
     no effect on matching, which is endian-agnostic.

  -v, --version

     Print version and exit.

  --color

     Colorize the output.

DETAILS:

     diff32 is an awk script wrapping the od and diff utilities
     that produces a human-readable side-by-side text summary of
     differences between two raw 32-bit binary files.

     diff32 searches for insertions, deletions, and co-located
     changes. By default, it will also perform fuzzy matching to
     align regions of similar content.

EXAMPLE:

  diff32 -d --color mips_binary1.bin mips_binary2.bin | less -R

     Produce a colorized summary of the differences in binary files
     mips_binar1.bin and mips_binary2.bin, presented on the terminal
     one page at a time using the 'less' utility. The -d option to
     diff32 requests extra time be spent to minimize the change
     set. The -R option instructs less to allow ANSI color codes.

AUTHOR:

     Written by Monty Montgomery <monty@xiph.org>
     This is free software: you are free to change and redistribute
     it.  There is NO WARRANTY, to the extent permitted by law.

SEE ALSO:

  od(1), diff(1), cmp(1), xdelta(1)
