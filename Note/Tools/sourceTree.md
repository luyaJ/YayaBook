## 1. sourcetree推送失败

sourcetree 推送时，在弹出框中输入 github 用户名和密码，但是推送失败，提示：`...sourcetree Logon failed, use ctrl+c to cancel basic credential prompt.`

原因：新版的 GIT 不再支持弹出框验证用户名密码的方式，所以推送请求被拒绝了。

解决办法：到[https://gitforwindows.org/](https://gitforwindows.org/) 下载最新版本的git， 安装好后重新推送， 就会引导你到浏览器中输入用户名密码，之后推送成功。

