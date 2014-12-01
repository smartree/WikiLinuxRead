zip vs gzip:

* zip和gzip(gz)不兼容，虽然它们都是使用相同的`deflate`压缩算法
* zip更像一个打包器，能把多个多件放到一个zip中；gzip一次只对一个文件压缩，通常与tar命令一起用


摘自http://www.netlib.org/gnu/gzip/readme


> zip is an archiver: it compresses several files into a single archive
> file. gzip is a simple compressor: each file is compressed separately.
> Both share the same compression and decompression code for the
> 'deflate' method.  unzip can also decompress old zip archives
> (implode, shrink and reduce methods). gunzip can also decompress files
> created by compress and pack. zip 1.9 and gzip do not support
> compression methods other than deflation. (zip 1.0 supports shrink and
> implode). Better compression methods may be added in future versions
> of gzip. zip will always stick to absolute compatibility with pkzip,
> it is thus constrained by PKWare, which is a commercial company.  The
> gzip header format is deliberately different from that of pkzip to
> avoid such a constraint.

> On Unix, gzip is mostly useful in combination with tar. GNU tar
> 1.11.2 has a -z option to invoke gzip automatically.  "tar -z"
> compresses better than zip, since gzip can then take advantage of
> redundancy between distinct files. The drawback is that you must
> scan the whole tar.gz file in order to extract a single file near
> the end; unzip can directly seek to the end of the zip file. There
> is no overhead when you extract the whole archive anyway.
> If a member of a .zip archive is damaged, other files can still
> be recovered. If a .tar.gz file is damaged, files beyond the failure
> point cannot be recovered. (Future versions of gzip will have
> error recovery features.)