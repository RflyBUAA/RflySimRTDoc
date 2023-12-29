# 如何贡献代码

本文文档使用MkDocs开发，配置简单。建议在WSL下进行开发。

!!! TIP "1. 安装文档环境可以参考[mkdocs.org](https://www.mkdocs.org)"

	1.1  `pip install mkdocs-pdf-export-plugin`之后在配置文件`mkdocs.yml`中启用插件
	```
	plugins:
		- pdf-export
	```

	1.2 `pip install pymdown-extensions`

	1.3 `pip install markdown-callouts`详见[https://github.com/sondregronas/mkdocs-callouts](https://github.com/sondregronas/mkdocs-callouts)

	1.4 `pip install mdx-gh-links`

	1.5 `pip install mkdocs-click`

	1.6 `pip install mkdocs-autorefs`

	1.7 `pip install mkdocstrings`和`pip install 'mkdocstrings[crystal,python]'`

	1.8 `pip install mkdocs-gitbook`

	1.9 `pip install mkdocs-with-pdf`
	```
	plugins:
		- with-pdf
	```

	1.10 `pip install markdown-checklist`
	```
	markdown_extensions:
		- markdown_checklist.extension
	```

	1.11 `pip install mkdocs-video`
	```
	plugins:
    	- mkdocs-video
	```

	1.12 `pip install mkdocs-git-revision-date-localized-plugin`
	```
	plugins:
  		- git-revision-date-localized
	```

	1.13 `pip install markdown-captions`与`pip install mkdocs-video`在使用中存在冲突
	```
	markdown_extensions:
  		- markdown_captions
	```

	1.14 `pip install mkdocs-resize-images`
	```
	plugins:
  		- resize-images
	```

	1.15 `pip install mkdocs-git-latest-changes-plugin`
	```
	plugins:
  		- git-latest-changes
	```
	即可显示最近几次提交涉及的更改。

	1.16 ` pip install mkdocs-latest-release-plugin`
	```
	plugins:
  		- git-latest-release
	```

!!! TIP "2. 配置Git用户"

	2.1 新安装的WSL首先配置Git用户信息
	```
	git config --global user.name "Your Name"
	git config --global user.email "email@example.com"
	```

	2.2 生成ssh key
	```
	ssh-keygen -t ed25519 -C "your_email@example.com"
	```
	或
	```
	ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
	```
	在输出的结果中可以看到类似这样的输出
	```
	Your public key has been saved in /home/kcx064/.ssh/id_ed25519.pub
	```
	运行cat命令查看.pub文件中的内容，例如
 	```
	cat /home/kcx064/.ssh/id_ed25519.pub
	```
	将输出的内容添加到github仓库的SSH keys中<br/>
	2.3 安装Git lfs
	```
	sudo apt-get install git-lfs
	```

!!! TIP "3. 修改文档内容"

    3.1 运行`git clone https://github.com/RflyBUAA/RflySimRTDoc.git`

    3.2 运行`git checkout master` (注意：默认分支可能是`gh-pages`, 开发前请确认当前分支不是`gh-pages`)

	3.3 修改文档，markdown格式

	3.4 运行`mkdocs build`，之后会在根目录下生成/更新`site`文件夹下的内容
    
    3.5 运行`mkdocs serve`可以本地预览效果

	3.6 运行`mkdocs gh-deploy`以提交site下的更改

	3.7 如果`mkdocs gh-deploy`本身没能自动将更改push到远端仓库，那么手动`git push origin gh-pages` 

	3.8 提交master分支的更改