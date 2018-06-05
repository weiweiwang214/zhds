```
1. ctrl + alt + s 打开setting窗口
2. 找到tools --> file watchers
3. 点击右侧的“+”号添加scss文件监听
4. 配置窗口配置项填写：

    Scope: Current File

    Program: D:\Ruby\Ruby22-x64\bin\scss.bat

    Argements: --no-cache --update --style expanded --trace  $FileName$:$FileParentDir$\css\$FileNameWithoutExtension$.css

    Output paths to refresh: $FileDir$

其中的Argements项的配置指令：
    --no-cache： 不需要缓存
    --update：实时更新
    --style expanded：压缩格式(nested：嵌套输出方式，最右的花括号跟在最后一个属性后面；expanded：展开输出方式，完全展开；compact：紧凑输出方式，一个类就是一行，compressed：压缩输出方式，整个文件压缩成一行)
    --trace 路由追踪

$FileName$:$FileParentDir$\css
当前文件夹的父文件夹下的css文件夹

注：scss文件中使用了中文导致报错
解决方案：
1. 在scss文件开始出设置文件编码格式：@charset "utf-8";
2. 配置项启用路由追踪 --trace

如果路径中有中文，则查看报错信息
如：D:\Ruby\Ruby22-x64\lib\ruby\gems\2.2.0\gems\sass-3.4.22\lib\sass\importers\filesystem.rb 87 index...
则打开D:\Ruby\Ruby22-x64\lib\ruby\gems\2.2.0\gems\sass-3.4.22\lib\sass\importers\filesystem.rb文件找到第87行：
把以下代码：
def remove_root(name)
    if name.index(@root + "/") == 0
        name[(@root.length + 1)..-1]
    else
        name
        end
    end
改为：(添加了：encode("utf-8", "gbk"))
def remove_root(name)
    if name.encode("utf-8", "gbk").index(@root + "/") == 0
        name[(@root.length + 1)..-1]
    else
        name
        end
    end
```