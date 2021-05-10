Name:      hello-world
Version:   1
Release:   1
Summary:   Most simple RPM package
License:   FIXME

%description
This is my first RPM package, which does nothing.

%prep
# we have no source, so nothing here

%build
cat > hello-world.sh << EOF
#!/usr/bin/bash
echo Hello world
EOF

%install
mkdir -p %{buildroot}/usr/bin/
install -m 755 hello-world.sh %{buildroot}/usr/bin/hello-world.sh

%files
/usr/bin/hello-world.sh

%changelog
# let skip this for now


rpm --eval %{?dist}


rpmdev-newspec bello



rpm --showrc


宏文件路径：/usr/lib/rpm/macros.d/


systemctl disable firewalld

systemctl enable vncserver@:1


valgrind --tool=memcheck --leak-check=full ./t6

ls -la /usr/lib64/liblfs*


rpm2cpio mlocate-0.22.2-2.i686.rpm | cpio –ivd usr/share/doc/mlocate-0.22.2/README 提取文件

rpm -h 显示进度
rpm -v 显示详细信息
rpm -vv 更加详细的信息

rpm -Uhvv

rpm -U --percent jikes-1.16-1.i386.rpm   --percent 显示百分比


rpm -U --test eruby-libs-0.9.8-2.i386.rpm 不安装仅进行测试 会检查包是否可以安装 并且显示依赖关系

--prefix  
--relocate  修改安装路径

rpm -U --root /tmp --dbpath /var/lib/rpm jikes-1.16-1.i386.rpm  --dbpath ，RPM数据库位于正常位置，/var/lib/rpm/  可能会导致安装出现问题 建议与  --badreloc  --relocate 一起使用


Freshening up 
rpm -F package_name  与 -U 功能类似 -F 要求之前安装过 其余相同


rpm -e --test syslinux-1.75-3 测试是否可以删除 （有其他包依赖于本包）

rpm -qa 查询所有安装包

rpm -qa | grep ssh、
与
rpm -qa --pipe "grep ssh" 等同


- rpm -qf
  ```
   # which grep 
   /bin/grep
   # rpm -qf /bin/grep
   grep-2.6.3-1
   或者干脆合并为一步
   rpm -qf `which grep`
   或者
   rpm -qf $(which grep)

  ```

- rpm 命令格式
  ```
  rpm –MajorOperation –extra_options packages_or_files
  ```

- rpm 查询已安装rpm包信息
  ```
  rpm -qi package
  ```

- rpm 查询安装包里面的文件
  ```
  rpm –ql package
  rpm -qlv package 更加详细的信息
  ```

- rpm 列出软件包的配置文件
  ```
  rpm –qc package_name
  ```

- rpm 列出软件包的文档文件
  ```
  rpm –qd package_name
  ```

- rpm 软件包中文件状态
  ```
  rpm –qs package_name
  ```
A
- rpm 列出安装脚本
  ```
  rpm -q --scripts package_name
  ```

- rpm 显示更改日志
  ```
    rpm –q --changelog package_name
  ```

- rpm 查找最近安装的包 排序
  ```
  rpm -qa --last | head
  ```

- rpm 查询不在本地包的信息
  ```
  rpm -qp ftp://username:password@hostname:port/path/to/rpm/file
  ```

- rpm 验证
  ```
  rpm -V verify_options package_name
  ```

- rpm 重建数据库
  ```
  rpm 数据存放在  /var/lib/rpm
  rpm --rebuilddb
  ```

- rpm 新建数据库
  ```
  rpm --initdb 如果已经出现了需要新建rpm数据库的情况 还不如直接重新安装操作系统
  ```

- rpm 查看包是否满足安装的条件
  ```
  rpm -qp --requires sendmail-8.12.5-7.i386.rpm
  ```

- rpm 提供的功能
  ```
   rpm -q --provides tcsh
  ```

- rpm 检查是否存在冲突
  ```
   rpm -q --conflicts httpd
  ```

- rpm 软件包被那些包依赖
  ```
  rpm -q --whatrequires tcsh
  ```

- rpm 查询哪个包提供了 webserver 的功能
  ```
  rpm -q --whatprovides webserver
  ```
- rpm rpmfind
  ```
  rpmfind package_name
  //todo
  ```

  - rpm rpmfind
  ```
  //todo
  ```

  - rpm rpm包网址
  ```
  rpmfind.net
  freshrpms.net
  http://rpm.pbone.net/ provides
  http://plf.zarb.org/
  www.math.unl.edu/~rdieter/Projects/
  www.rpmhelp.net/
  www.aucs.org/rpmcenter/
  www.owlriver.com/projects/links/
  ```

- rpm AutoRPM
  ```
  //todo
  ```


valgrind --tool=memcheck --leak-check=full --log-file=log.txt ./TESTMANAGER

- rpmbuild 构建命令 (一般只会使用 -ba 命令)
  ```
  rpmbuild -bBuildStage spec_file
  -ba          Build all, both a binary and source RPM
  -bb          Build a binary RPM
  -bc          Build (compile) the program but do not make the full RPM, stopping just after the %build section
  -bp          Prepare for building a binary RPM, and stop just after the %prep section
  -bi          Create a binary RPM and stop just after the %install section
  -bl          Check the listing of files for the RPM and generate errors if the buildroot is missing any of the files to be installed
  -bs          Build a source RPM only
  ```

- rpmbuild 使用rpmbuild 操作时 不要使用root用户 使用普通用户就可以

- rpmbuild clean
  ```
  rpmbuild --clean specfile
  ```

- rpmbuild 验证  
  ```  
  rpmbuild –bl spec_file
  ```

- rpmbuild 初始化目录
  ```
  rpmdev-setuptree
  ```


- rpmbuild clean
  ```
  $ rpmbuild --clean /usr/src/redhat/SPECS/jikes.spec  清理树 
  ```

- rpmbuild 架构
  ```
  rpmbuild -bi --target i486-redhat-linux    cpu-vendor-os （cpu 供应商 操作系统）
  ```

- rpmbuild 直接通过tar包构建
  ```
  rpmbuild -tBuildStage compressed_tar_archive  (rpmbuild -ta kernel-4.19.5.tar.gz ) 
  ```
- rpmbuild 用源码rpm包重新构建  --rebuild
  ```
  rpmbuild --rebuild unix2dos-2.2-17.src.rpm
  ```

- rpm 同时安装多个包
  ```
  rpm -ihv package1.rpm package2.rpm package3.rpm  如果有一个安装失败 那么全部都不会安装
  ```

- rpm 回滚
  ```
  rpm –U --rollback "3 months ago" 
  ```

- rpm 查找包
  ```
  rpmfind package_name
  ```

- rpm 模糊查询
  ```
   rpmfind --apropos "mail client"
  ```

- rpm rpm包查找网站
  ```
   rpmfind.net
   freshrpms.net
   http://rpm.pbone.net/
   http://plf.zarb.org/
   www.math.unl.edu/~rdieter/Projects/
   www.rpmhelp.net/
   www.aucs.org/rpmcenter/
   www.owlriver.com/projects/links/
  ```

- rpmbuild clean
  ```
  $ rpmbuild --clean /usr/src/redhat/SPECS/jikes.spec  清理树 
  ```

- rpmbuild 架构
  ```
  rpmbuild -bi --target i486-redhat-linux    cpu-vendor-os （cpu 供应商 操作系统）
  ```

- rpmbuild 直接通过tar包构建
  ```
  rpmbuild -tBuildStage compressed_tar_archive  (rpmbuild -ta kernel-4.19.5.tar.gz ) 
  ```
- rpmbuild 用源码rpm包重新构建  --rebuild
  ```
  rpmbuild --rebuild unix2dos-2.2-17.src.rpm
  ```

- 解决rpm依赖问题
  ```
  yum-builddep 
  ```


- rpmbuild 需要工具
  ```
  yum install gcc rpm-build rpm-devel rpmlint make python bash coreutils diffutils patch rpmdevtools
  ```

- 一个简单的spec 文件
  ```
  Name: hello-world 
  Version: 1 
  Release: 1 
  Summary: Most simple RPM package 
  License: FIXME 
  %description This is my first RPM package, which does nothing. 
  %prep # we have no source, so nothing here %build cat > hello-world.sh <<EOF 
  #!/usr/bin/bash 
  echo Hello world 
  EOF 
  %install 
  mkdir -p %{buildroot}/usr/bin/ 
  install -m 755 hello-world.sh %{buildroot}/usr/bin/hello-world.sh 
  %files 
  /usr/bin/hello-world.sh 
  %changelog 
  # let skip this for now
  ```

- 运行 rpmdev-setuptree 在当前用户的家目录下生成 rpmbuild 目录
  
- 运行 rpmbuild -ba hello-world.spec 生成自己的第一个包

- 生成patch文件 diff -Naur cello.c.orig cello.c > cello-output-first-patch.patch

- 源码用补丁修改  patch < cello-output-first-patch.patch

- 安装程序  sudo install -m 0755 bello /usr/bin/bello （-m 自定义模式）


- rpmbuild 目录结构
  ```
  SPECS	        %_specdir	Spec 文件目录	        保存 RPM 包配置、规范（.spec）文件
  SOURCES	        %_sourcedir	源代码目录	        源代码/补丁文件
  BUILD  	        %_builddir	构建目录	                源码包被解压至此，并在该目录的子目录完成编译
  BUILDROOT	%_buildrootdir	最终安装目录	        保存 %install 阶段安装的文件
  RPMS	        %_rpmdir	标准 RPM 包目录	        生成/保存二进制 RPM 包
  SRPMS	        %_srcrpmdir	源代码 RPM 包目录	生成/保存源码 RPM 包(SRPM)
  ```

- NVR 原则
  ```
  rpm 包命名遵循NVR原则 NAME-VERSION-RELEASE python-2.7.5-34.el7.x86_64
  ```

- spec 文件详细参数
  |参数|描述|
  |----|----|
  |Name|程序包的名称 与spce文件名应一直
  |Version|软件版本|
  |Release|此版本的软件发布测试|
  |Summary|简要说明|
  |License|软件许可证|
  |URL|更多信息完整的URL|
  |Source0|源代码压缩存档的路径 序号可以累加 Source1 Source2|
  |Patch0|补丁名称 可以累加 Patch1 Patch2|
  |BuildArch|系统架构|
  |BuildRequires|安装所需要的依赖包|
  |Requires|运行需要依赖包|
  |ExcludeArch|排除某个系统架构|
  |%description|软件包的完整描述 可以分段落 跨越多行|
  |%prep|如何构建环境 可以包含shell脚本
  |%build|实际构建软件包的命令|
  |%install|从%builddir（生成的位置）复制到%buildroot目录|
  |%check|软件包的测试命令|
  |%files|将安装在最终用户系统中的文件的列表。|
  |%changelog|不同版本或发行版本之间对包发生的更改记录。|

- rpmdev-newspec 创建spec文件

- rpmbuild -bs SPECFILE 构建SRPM

- 构建 PRM rpmbuild --rebuild 通过src.rpm

- 安装 rpm -Uvh 

- Building Binary from the SPEC file
  ```
  rpmbuild -bb ~/rpmbuild/SPECS/bello.spec
  ```
- rpm 检查
  ```
  rpmlint 
  ```

- 添加签名
  ```
  rpm --addsign
  ```

- 检查签名
  ```
  rpm --addsign blather-7.9-1.i386.rpm 
  ```


- rpm 条件判断
  ```
  %if expression 
  ... 
  %else 
  ... 
  %endif
  ```

- 判断系统架构
  ```
  %ifarch i386 sparc 
  ... 
  %endif
  ```

- 判断操作系统
  ```
  %ifos linux 
  ... 
  %endif
  ```
make rpm-pkg

cap 15

ls -la /usr/lib64/liblfs*

