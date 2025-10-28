- **Lossy** compression 
	- is very effective in reducing the size of files, but the integrity of the information is lost :
	- mp3, .mp4, .png, and .jpg are all lossy compression algorithms
	- lossy compression is unacceptable when you’re sending files or software and data integrity is crucial 
- **lossless** compression is not as efficient as lossy compression
___
- the first thing you do when compressing files is to combine them into an archive
- use [[tar]] command`(tape archive)
- `tar -cvf file.tar file1 file2 file3` : c:creat/v:verbose/f:read/write
- `tar -xf file.tar`
### Compressing file
- **commands :** 
	- [[gzip]] (most used), which uses the extension .$tar.gz or .tgz$
	- [[bzip2]] (slowest,smaller) , which uses the extension $.tar.bz2$
	- [[compress]] (fastest,larger) , which uses the extension $.tar.z$
- **[[compress]]** : `sudo gzip file.*`
- **[[decompress]]** : `gunzip file.*`
___
- `dd if=inputfile of=outputfile` : [[dd]] command makes a [[bit-by-bit copy]] of a file, a filesystem, or even an entire hard drive
- the `noerror` option continues to copy even if errors are encountered. The `bs` option allows you to determine the block size (the number of bytes read or written per block)
- `dd if=/dev/media of=/root/flashcopy bs=4096 conv=noerror`
- 