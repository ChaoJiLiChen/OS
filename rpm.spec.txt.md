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

- rpm 列出安装脚本
  ```
  rpm -q --scripts package_name
  ```

- rpm 显示更改日志
  ```
    rpm –q --changelog package_name
  ```