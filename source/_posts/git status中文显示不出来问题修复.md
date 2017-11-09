---
title: "git status中文显示不对问题修复"
date: 2017年11月 7日 星期二 16时20分51秒 CST
tags: git
author: chenchuanyin
---

如题，我的mac上git status显示
```text
➜  hexo git:(master) ✗ gst
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
  (commit or discard the untracked or modified content in submodules)

	modified:   _config.yml
	modified:   package-lock.json
	modified:   package.json
	deleted:    source/_posts/hello-world.md
	deleted:    "source/_posts/\346\265\213\350\257\225\344\275\277\347\224\250-md.md"
	deleted:    "source/_posts/\347\254\254\344\272\214\344\270\252\346\265\213\350\257\225.md"
	modified:   themes/maupassant (modified content)
	modified:   themes/next (untracked content)

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	"source/_posts/emacs\346\217\222\345\205\245\345\275\223\345\211\215\346\227\266\351\227\264\346\210\263.md"
	"source/_posts/\344\277\256\345\244\215GO\345\214\205\347\256\241\347\220\206\345\267\245\345\205\267GLIDE\344\270\215\350\203\275\350\256\277\351\227\256golang.org\347\232\204\346\233\277\344\273\243\346\226\271\346\241\210.md"
	source/about/

no changes added to commit (use "git add" and/or "git commit -a")
```

修复方法：
```code
#不对0x80以上的字符进行quote，解决git status/commit时中文文件名乱码
git config --global core.quotepath false
```

再次git status就显示OK了。
```text
➜  hexo git:(master) ✗ gst
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
  (commit or discard the untracked or modified content in submodules)

	modified:   _config.yml
	modified:   package-lock.json
	modified:   package.json
	deleted:    source/_posts/hello-world.md
	deleted:    source/_posts/测试使用-md.md
	deleted:    source/_posts/第二个测试.md
	modified:   themes/maupassant (modified content)
	modified:   themes/next (untracked content)

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	source/_posts/emacs插入当前时间戳.md
	source/_posts/修复GO包管理工具GLIDE不能访问golang.org的替代方案.md
	source/about/

no changes added to commit (use "git add" and/or "git commit -a")
```
