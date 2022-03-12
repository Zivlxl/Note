##### svn命令的使用

1. checkout

   svn checkout svn:// + address （将address 上的目录checkout到本地目录）

   简写成 svn co 

2. add

   svn add xxx.file (将xxx.file 添加)

3. commit

   svn commit -m "LogMessage" [-N] [--no-unlock] PATH(如果选择了保持锁，就使用--no-unlock开关)

   将改动你的文件提交到版本库

   简写成 svn ci

4. lock/unlock

   svn lock -m "LockMessage" [--force] PATH

   svn unlock PATH (加锁/解锁)

5. update

   svn update如果后面没有目录，默认将当前目录以及子目录下的所有文件都更新到最新版本。
   svn update -r 200 test.php(将版本库中的文件test.php还原到版本200)
   svn update test.php(更新，于版本库同步。如果在提交的时候提示过期的话，是因为冲突，需要先update，修改文件，然后清除svn resolved，最后再提交commit)

   简写成 svn up

6. status

   svn status PATH （目录下的文件和子目录的状态，正常状态不显示）
   不在svn的控制中；M：内容被修改；C：发生冲突；A：预定加入到版本库；K：被锁定

   svn status -v PATH(显示文件和子目录状态)
   第一列保持相同，第二列显示工作版本号，第三和第四列显示最后一次修改的版本号和修改人。

   (查看文件或者目录状态)

   简写成 svn st

7. delete

   svn delete path -m "delete test fle"
   例如：svn delete svn://192.168.1.1/pro/domain/test.php -m "delete test file"
   或者直接svn delete test.php 然后再svn ci -m 'delete test file‘，推荐使用这种

   简写成 svn （del, remove, rm）

8. log

   svn log PATH (查看日志)

   svn log -r {yyy-MM-d}:{yyy-MM-d} （查看一段日期的日志）

9. diff

   svn diff PATH (比较差异，将修改的文件与基础版本比较)

   svn diff -r m:n PATH （对比版本m和版本n之间的差异）

10. info

    svnn info PATH（查看文件详细信息）

11. merge

    svn merge -r m:n PATH （将两个版本的差异合并到当前文件PATH）

12. help

    svn help

    svn help ci（查看帮助）

13. list

    svn list PATH  （显示PATH目录下所有属于版本库的文件和目录）

    简写成 svn ls

14. 

