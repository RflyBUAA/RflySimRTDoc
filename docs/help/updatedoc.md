# 如何贡献代码

本文文档使用MkDocs开发，配置简单。建议在WSL下进行开发。

1. 安装文档环境可以参考[mkdocs.org](https://www.mkdocs.org)

2. 修改文档内容

    2.1 运行`git clone https://github.com/RflyBUAA/RflySimRTDoc.git`

    2.2 运行`git checkout master` (注意：默认分支是gh-pages, 所以需要手动切换)
    
    2.3 运行`mkdocs serve`可以本地预览效果

3. 运行`mkdocs build`，之后会在根目录下生成/更新`site`文件夹下的内容

4. 运行`mkdocs gh-deploy`以提交site下的更改

5. 如果`mkdocs gh-deploy`本身没能自动将更改push到远端仓库，那么手动`git push origin gh-pages` 

6. 提交master分支的更改