# ftpput

# 用法
` ftpput.sh <FTPServerAddress> <FTP_UserName> <FTP_Password> <MainTargetPath> <local_dir/filename> <remote_dir> `

` ftpput.sh $ftp_ip $ftp_username $ftp_psw $TargetPath $upload_file $remote_dir `


# 申明
由于需要在云编译中实现无交互FTP上传文件，故采取本脚本方式。

### 为何把服务器，用户名，密码等参数全部拿出来，而不是直接写在脚本里：
- 1. 方便随时更换目标服务器
- 2. 方便用于Github云编译，隐藏敏感信息（搭配Secrets使用）

### 本脚本可实现：

登录到目标FTP服务器[$ftp_ip]，

cd进入目标目录[$TargetPath]，

创建以[当前日期]为名的文件夹，

把本地文件[$upload_file]，

上传到该目录[$remote_dir][通常直接写./来实现上传到刚创建的日期名文件夹内，为扩大可操作性，本路径值可按需求变动]


# 本脚本优势：

由于ftp命令的简陋性，经常遇到上传完成但无返回，导致自动化脚本一直停留等待的问题。故可利用本脚本，实现在后台上传，可搭配timeout设定，强制关闭ftp进程。（高级用户可进行对比源/目标的sha256值，以判断是否需要掐断再重新上传）

调用参考：

` ftpput.sh $ftp_ip $ftp_username $ftp_psw $TargetPath $upload_file $remote_dir > ftp.log 2>&1 & `

` sleep 600 `

` killall -9 ftp `

本脚本依赖ftp，
`yum install ftp -y`
或 `apt install ftp -y`
来安装，具体请参考运行环境。
