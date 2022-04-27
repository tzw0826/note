#### 			GitHub

1. 配置密钥：ssh-keygen -t rsa

2. 同步到远程仓库：git remote add origin git@github.com:远程仓库名称.git

   ​							   （git push -u origin master）

3. 克隆远程仓库：git clone git@github.com:远程仓库名字.git

3. 删除文件：git rm

3. 删除文件夹：git rm -r

4. GitHub常用词含义

   - watch：会持续受到项目的动态
   - fork：复制某个项目到自己的仓库
   - star：点赞数
   - clone：将项目下载到本地
   - follow：关注你感兴趣的作者，会收到他们的动态

5. GitHub搜索技巧 - 找开发者

   1. location:
      - location:china，匹配用户填写的地址在china
   2. language:
      - language:java，匹配开发语言为Java的开发者
   3. followers:
      - fllowers:>=1000，匹配拥有超过1000名关注者的开发者
   4. in:funllname:
      - jack in:funllname，匹配用户实名为jack的开发者

6. GitHub搜索技巧 - 找项目

   1. Awesome + 关键字
   2. stars：
      - stars:>=500，匹配收藏数量超过500的项目
   3. language:
      - language:java，匹配以java作为开发语言的项目
   4. forks:
      - forks:>=500，匹配分支数量超过500的项目