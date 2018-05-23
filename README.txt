ozip functionality mimics gzip/bzip2.

usage:
ozip [file] [opts]             (compresses)
ozip [file] [-d opts]          (decompress)

without file args ozip defaults to stdin/stdout compression.
uses .ooz extension for compressed files.

(!) Deletes input files unless -k --keep opt is used (as does gzip).

compress\or selection: --kraken -mk
                       --leviathan -ml
                       --selkie -ms
                       --mermaid -mm
