Git  版本控制器

记录文件的更新迭代, 每次修改了什么内容, 进行版本控制. 且支持各种类型的文件

文件需要在Git仓库中,

![image-20230925193711200](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20230925193711200.png)



tree ./.git

初始化仓库/ 创建本地仓库 git init

下一步  需要配置两个配置项  一个是name  一个是email  不配置之后可能会报错

![image-20230925194303321](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20230925194303321.png)

![image-20230925194543831](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20230925194543831.png)

--global : 一个服务器上可能有多个git仓库, --global就是在当前服务器上的所有仓库都生效这个name和email

实际上, .git文件才是本地仓库, 又名版本库



![image-20230925201342086](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20230925201342086.png)

演示git add git  commit  ,还有之前没见过的git log

![image-20230925201614178](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20230925201614178.png)

![image-20230925201738146](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20230925201738146.png)

查看git 对象里的内容, 不能直接cat, 要git cat

![image-20230925201840170](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20230925201840170.png)

![image-20230925201927436](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20230925201927436.png)

![image-20230925202008794](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20230925202008794.png)

git 就是通过对象记录文件的修改, 也就是具体的版本迭代的内容

![image-20230925202911047](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20230925202911047.png)

git diff 显示暂存区和工作区的差异

![image-20230925203036444](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20230925203036444.png)

![image-20230925203106481](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20230925203106481.png)



---

版本回退

![image-20230926142503571](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20230926142503571.png)

![image-20230926142741571](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20230926142741571.png)





----

删除文件



![image-20230926145322308](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20230926145322308.png)

这是使用git rm![image-20230926145356770](C:\Users\yangzilong\AppData\Roaming\Typora\typora-user-images\image-20230926145356770.png)

这是三步, 也就是把工作区rm 然后add上传到暂存区