语言：中文 
> 该主题根据Hugo PaperMod主题修改而来: https://github.com/adityatelange/hugo-PaperMod

### [博客DEMO](https://eddycliff.github.io/)

## 1. git clone 拉取代码

① 用`git clone`的方式拉取代码至桌面，此时会在桌面生成EddyBlogCode目录

② 进入到EddyBlogCode目录，输入`git submodule update --init`，表示拉取themes/hugo-PaperMod/下的子模块，里面放的是官方主题

## 2. 启动界面

③ 把目录定位到EddyBlogCode下，在终端输入`hugo server -D`，在浏览器输入：localhost:1313 即可看到现成的博客模板。

## 3. 修改信息

模板内部有许多个人信息需要自己配置，请耐心修改完，可以参考Sulv大佬的建站教程：[https://www.sulvblog.cn/posts/blog/](https://www.sulvblog.cn/posts/blog/) 还有我的建站教程[https://eddyblog.cn/tags/hugo%E7%BD%91%E7%AB%99%E6%90%AD%E5%BB%BA/](https://eddyblog.cn/tags/hugo%E7%BD%91%E7%AB%99%E6%90%AD%E5%BB%BA/)


## 4. shortcodes使用方法

`bilibili: {{< bilibili BV1Fh411e7ZH(填 bvid) >}}`

`youtube: {{< youtube w7Ft2ymGmfc >}}`

`ppt: {{< ppt src="网址" >}}`

`douban: {{< douban src="网址" >}}`

```
# 文章内链卡片
# 末尾要加 md，只能填写相对路径，如下
{{< innerlink src="posts/tech/mysql_1.md" >}}
```

```
gallery:

{{< gallery >}}
{{< figure src="https://www.eddyblog.cn/img/logo1.png" >}}
{{< figure src="https://www.eddyblog.cn/img/logo1.png" >}}
{{< /gallery >}}
```

## 5. 可能遇到的问题

- 有些使用者会部署到`github`，输入`git add -A`命令后，如提示`warning:LF will be replaced by CRLF in ******`，这时可以不用管，没有什么实际影响，继续`git commit`.