# GitHub生成Token

登录github官网，按以下图片步骤点击（其中repo必选）

[![getToken](/getToken.jpg)](/getToken.jpg)

创建后生成的token要保存好，只有创建时可见

**通过令牌访问代码库**

\<token\> -- 创建好的令牌

\<username\> -- github的用户名

\<reponame\> -- 远程仓库名

```sh
git remote set-url origin https://<token>@github.com/<username>/<reponame>.git
```

**首次clone代码**

```sh
git clone https://<token>@github.com/<username>/<reponame>.git
```