<!-- @format -->

# 7z、7zip 命令行参数详解

对于一些使用库压缩、解压缩的操作,可以通过调用命令行去调用 7z 程序代替更方便,特别是应对各种不同格式的压缩包

下面是一些命令行 7z 程序的参数及翻译:

```
<Commands>
  a : Add files to archive
  b : Benchmark
  d : Delete files from archive
  e : Extract files from archive (without using directory names)
  h : Calculate hash values for files
  i : Show information about supported formats
  l : List contents of archive
  rn : Rename files in archive
  t : Test integrity of archive
  u : Update files to archive
  x : eXtract files with full paths

<Switches>
  -- : Stop switches and @listfile parsing
  -ai[r[-|0]]{@listfile|!wildcard} : Include archives
  -ax[r[-|0]]{@listfile|!wildcard} : eXclude archives
  -ao{a|s|t|u} : set Overwrite mode
  -an : disable archive_name field
  -bb[0-3] : set output log level
  -bd : disable progress indicator
  -bs{o|e|p}{0|1|2} : set output stream for output/error/progress line
  -bt : show execution time statistics
  -i[r[-|0]]{@listfile|!wildcard} : Include filenames
  -m{Parameters} : set compression Method
    -mmt[N] : set number of CPU threads
    -mx[N] : set compression level: -mx1 (fastest) ... -mx9 (ultra)
  -o{Directory} : set Output directory
  -p{Password} : set Password
  -r[-|0] : Recurse subdirectories for name search
  -sa{a|e|s} : set Archive name mode
  -scc{UTF-8|WIN|DOS} : set charset for for console input/output
  -scs{UTF-8|UTF-16LE|UTF-16BE|WIN|DOS|{id}} : set charset for list files
  -scrc[CRC32|CRC64|SHA1|SHA256|*] : set hash function for x, e, h commands
  -sdel : delete files after compression
  -seml[.] : send archive by email
  -sfx[{name}] : Create SFX archive
  -si[{name}] : read data from stdin
  -slp : set Large Pages mode
  -slt : show technical information for l (List) command
  -snh : store hard links as links
  -snl : store symbolic links as links
  -sni : store NT security information
  -sns[-] : store NTFS alternate streams
  -so : write data to stdout
  -spd : disable wildcard matching for file names
  -spe : eliminate duplication of root folder for extract command
  -spf : use fully qualified file paths
  -ssc[-] : set sensitive case mode
  -sse : stop archive creating, if it can't open some input file
  -ssp : do not change Last Access Time of source files while archiving
  -ssw : compress shared files
  -stl : set archive timestamp from the most recently modified file
  -stm{HexMask} : set CPU thread affinity mask (hexadecimal number)
  -stx{Type} : exclude archive type
  -t{Type} : Set type of archive
  -u[-][p#][q#][r#][x#][y#][z#][!newArchiveName] : Update options
  -v{Size}[b|k|m|g] : Create volumes
  -w[{path}] : assign Work directory. Empty path means a temporary directory
  -x[r[-|0]]{@listfile|!wildcard} : eXclude filenames
  -y : assume Yes on all queries
```

```
<Commands>
  a : 向存档中添加文件
  b : 基准测试
  d : 从存档中删除文件
  e : 从存档中提取文件（不使用目录名）
  h : 计算文件的哈希值
  i : 显示支持的格式信息
  l : 列出存档的内容
  rn : 重命名存档中的文件
  t : 检查存档的完整性
  u : 更新存档中的文件
  x : 提取文件（包含完整路径）

<Switches>
  -- : 停止解析开关和@listfile
  -ai[r[-|0]]{@listfile|!wildcard} : 包括存档
  -ax[r[-|0]]{@listfile|!wildcard} : 排除存档
  -ao{a|s|t|u} : 设置覆盖模式
  -an : 禁用archive_name字段
  -bb[0-3] : 设置输出日志级别
  -bd : 禁用进度指示器
  -bs{o|e|p}{0|1|2} : 设置输出流的输出/错误/进度行
  -bt : 显示执行时间统计信息
  -i[r[-|0]]{@listfile|!wildcard} : 包括文件名
  -m{Parameters} : 设置压缩方法
    -mmt[N] : 设置CPU线程数
    -mx[N] : 设置压缩级别:-mx1（最快）... -mx9（极限）
  -o{Directory} : 设置输出目录
  -p{Password} : 设置密码
  -r[-|0] : 递归搜索子目录
  -sa{a|e|s} : 设置存档名称模式
  -scc{UTF-8|WIN|DOS} : 设置控制台输入/输出的字符集
  -scs{UTF-8|UTF-16LE|UTF-16BE|WIN|DOS|{id}} : 设置列表文件的字符集
  -scrc[CRC32|CRC64|SHA1|SHA256|*] : 设置x、e、h命令的哈希函数
  -sdel : 压缩后删除文件
  -seml[.] : 通过电子邮件发送存档
  -sfx[{name}] : 创建自解压存档
  -si[{name}] : 从标准输入读取数据
  -slp : 设置大页模式
  -slt : 显示l（列表）命令的技术信息
  -snh : 存储硬链接为链接
  -snl : 存储符号链接为链接
  -sni : 存储NT安全信息
  -sns[-] : 存储NTFS备用流
  -so : 将数据写入标准输出
  -spd : 禁用文件名的通配符匹配
  -spe : 提取命令时消除根文件夹的重复
  -spf : 使用完全限定的文件路径
  -ssc[-] : 设置大小写敏感模式
  -sse : 如果无法打开某些输入文件,则停止创建存档
  -ssp : 在存档时不更改源文件的最后访问时间
  -ssw : 压缩共享文件
  -stl : 从最近修改的文件中设置存档时间戳
  -stm{HexMask} : 设置CPU线程关联掩码（十六进制数）
  -stx{Type} : 排除存档类型
  -t{Type} : 设置存档类型
  -u[-][p#][q#][r#][x#][y#][z#][!newArchiveName] : 更新选项
  -v{Size}[b|k|m|g] : 创建卷
  -w[{path}] : 指定工作目录.空路径表示临时目录
  -x[r[-|0]]{@listfile|!wildcard} : 排除文件名
  -y : 对所有查询假定为是

```
