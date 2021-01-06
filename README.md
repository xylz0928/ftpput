# ftpput

# 用法 / Usage

` wget -O ftpput.sh git.io/FTPPut && chmod +x ftpput.sh `

` ftpput.sh <FTPServerAddress> <FTP_UserName> <FTP_Password> <MainTargetPath> <local_dir/filename> <remote_dir> `

` ftpput.sh $ftp_ip $ftp_username $ftp_psw $TargetPath $upload_file $remote_dir `

`code` 

# 申明 / Main

由于需要在云编译中实现无交互FTP上传文件，故采取本脚本方式。[亦可用于任意Linux系统]

To upload files in Github Actions with FTP (without inter actions), I create this bash script.[Also can be used on any Linux env.]
<br><br>
### 为何把服务器，用户名，密码等参数全部拿出来，而不是直接写在脚本里：
### Why put the RemoteSrv, FTP_Username, FTP_Password as parameters instead of directly set inside of bash:

- 方便随时更换目标服务器 / To eaily change target FTP Server
- 方便用于Github云编译，隐藏敏感信息（搭配Secrets使用）/ To be easy using in Github Actions, can hide secrets parameters(work together with Github Secrets)
<br><br>
# 本脚本可实现 / This script is to :
<br>
使用FTP用户名 ` $ftp_username `，
<br>
`code` 
Use FTP Username ` $ftp_username ` ,
<br><br>
以及FTP密码 ` $ftp_psw` ，
<br>
and FTP Password ` $ftp_psw` ,
<br><br>
登录到目标FTP服务器 ` $ftp_ip` ，
<br>
To logon to FTP Server ` $ftp_ip` ,
<br><br>
cd进入目标目录 ` $TargetPath` ，
<br>
cd to enter target remote path ` $TargetPath` ,
<br><br>
创建以 ` 当前日期`  为名的文件夹，
<br>
create folder named with ` current date` ,
<br><br>
把本地文件 ` $upload_file` ，
<br>
Put local file ` $upload_file` ,
<br><br>
上传到该目录 ` $remote_dir` 
<br>
通常直接写` ./` 来实现上传到刚创建的日期名文件夹内，为扩大可操作性，本路径值可按需求变动
<br><br>
Upload to the folder [$remote_dir] 
<br>
usually we can set as ` ./`  to upload file to created folder named as currect date, to be more flexible, I let the parameter can be set by you own
<br><br>


# 本脚本优势 / Advantage :

由于ftp命令的简陋性，经常遇到上传完成但无返回，导致自动化脚本一直停留等待的问题。故可利用本脚本，实现在后台上传，可搭配timeout设定，强制关闭ftp进程。（高级用户可进行对比源/目标的sha256值，以判断是否需要掐断再重新上传）

Due to the simple function of FTP command, it sometimes stucks without RETURN when finished, cause the whole autoscript always waiting for FTP process.
So with this script, it can support to be able to put ftp upload in background, with some timeout settings, force kill ftp progress.


调用参考 / Example :

` ftpput.sh $ftp_ip $ftp_username $ftp_psw $TargetPath $upload_file $remote_dir > ftp.log 2>&1 & `

` sleep 600 `

` killall -9 ftp `

本脚本依赖ftp，
This script requires ftp commmand,

`yum install ftp -y`
或/OR `apt install ftp -y`

来安装，具体请参考运行环境。
to install, pls reference with target running env.
