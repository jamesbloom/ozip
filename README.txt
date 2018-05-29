OZIP ver. 0.0.7

ozip functionality mimics gzip/bzip2.

usage:
ozip [file] [opts]             (compresses)
ozip [file] [-d opts]          (decompress)

without file args ozip defaults to stdin/stdout compression.
uses .ooz extension for compressed files.

(!) Deletes input files unless -k --keep opt is used (as does gzip).

Default compression settings are Oodle Kraken at Compression Level Normal (4).

compress\or selection: --kraken -mk
                       --leviathan -ml
                       --selkie -ms
                       --mermaid -mm
                       
level:   -1 -2 ... -8...

Full Options:
    -H                      prints Oodle compressor options help
		-c --stdout	            outputs to stdout (decompress only). 
		-d --decompress         decompress
		-z --compress           compress
		-k --keep               keep original file (otherwise deleted)
		-f --force              overwrite output file if exists
		-F --fast               low latency streaming compression
		-b --best               best compression. Long compress times.
		-t --test               tests existing compressed file validity
		-K --verify             verify file during compression
		-q --quiet              no prints
		-v --verbose            prints lots
		-s --small              low memory use ~2.5MB  (compression only)
		-(1-9)	                compression level 1-9
		-m[k] --compressor=[k]  [k/l/m/s] Oodle compressor selection
		--kraken --mermaid --selkie --leviathan     Oodle compressor choice
		--bufferlimit=[1-256]   (MB) max buffer size for compression.
		--blocklimit=[8+]       (KB) minimum block size in KB for streaming
		--contextlimit=[8+]     (KB) context limit KB. trades memory use for ratio

Unix only:
		--timeout=[1000]		time in ms to wait on inactve stdin during compression
    
    
