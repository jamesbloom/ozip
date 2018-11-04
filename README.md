
# OZIP
**Ozip** is a simple compression utility utilizing the Oodle high performance compression library.  Ozip's functionality mimics gzip; most invocations function identically. Like gzip, Ozip supports streaming compression/decompression from stdin to stdout. Builds on Windows, Linux and Mac.  
Ozip requires the Oodle SDK.  
# Usage    

ozip [file] [opts]&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; (compresses)  
ozip [file] [-d opts]&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; (decompress)  

* without file args ozip defaults to stdin/stdout compression.  
* uses .ooz extension for compressed files.  
* (!)Deletes input files unless -k --keep opt is used (as does gzip).  
* Ozip iterates on multiple file targets. To combine files, compose with tar (e.g. tar <files> | ozip > "archivedfiles.tar.ooz")

Default compression settings are Oodle Kraken at Compression Level Normal (4).  

# Settings  
Compressor selection:  
                      --kraken -mk  
                      --leviathan -ml  
                      --selkie -ms  
                       --mermaid -mm  
               	       --hydra -mh  
     *Kraken provides a balance of ratio and speed.   
     Leviathan provides maximum compression.    
     Selkie and Mermaid are even faster.                    
     Hydra can hit performance targets between those choices.  
     For more info see http://www.radgametools.com/oodlecompressors.htm*  

		       
compression effort level:     
          -1 -2  ...  -9
negative levels (-4 to -1) are HyperFasts and can be set with "-ol" option (eg. -ol-2)
*Higher effort levels get a better compression ratio at the expense of encode time*

More Options  
  
-H                     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *prints Oodle compressor options help*  
-c --stdout	        
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *outputs to stdout (decompress only).*    
-d --decompress         
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *decompress*   
-z --compress           
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *compress*  
-k --keep               
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *keep original file (otherwise deleted)*      
-f --force              
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *overwrite output file if exists*  
-F --fast              
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *low latency streaming compression*  
-b --best              
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *best compression. Long compress times.*  
-t --test              
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *tests existing compressed file validity*    
-K --verify           
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *verify file during compression*     
-q --quiet           
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *no prints*  
-v --verbose         
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *prints lots*  
-s --small          
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *low memory use ~2.5MB  (compression only)*   
--bufferlimit=[1-256]  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *(MB) max buffer size for compression.*  
--blocklimit=[8+]      
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *(KB) minimum block size in KB for streaming*  
--contextlimit=[8+]     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *(KB) context limit KB. trades memory use for ratio*   

Unix only:   
--timeout=[1000]        
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *time in ms to wait on inactve stdin during compression*  


Additional Oodle Compression options displayed with -H. See the Oodle Data Documentation for details.   

# Streaming 

Ozip supports nonblocking stream on linux, otherwise reading for EOF until bufferlimit. Setting a smaller blocklimit represents less tolerance for timeouts on linux, triggering a block to encode with less received data. Lower latency can also be achieved on all platforms by setting smaller max buffer size at the cost of compression ratio (this also lowers memory use)

# Headers 

Ozip adds a file header and block header to compressed data stream. Values are little endian.  
File Header Version 1:   16 bytes.      
4 byte "OZIP" magic word.  
4 byte Header Version.   
8 byte filesize (=0 if unknown when streaming.)   

Block Header Version 1:  16 bytes.    
4 byte "OZIP" magic word.  
4 bytes raw block size.  
4 bytes context size.  
4 bytes compressed size.  

# About   
OZIP ver. 0.1.1   

Ozip originally developed by:   
https://github.com/jamesbloom/ozip   
jamesbloom@gmail.com    
    
About the Oodle SDK:    
http://www.radgametools.com/oodle.htm   
    
