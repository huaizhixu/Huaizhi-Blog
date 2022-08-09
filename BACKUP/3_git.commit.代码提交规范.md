# [git commit 代码提交规范](https://github.com/huaizhixu/Huaizhi-Blog/issues/3)

##### 格式：
```
type(scope) : subject

```
( 1 ) type（必须） : commit 的类别，只允许使用下面几个标识：

-   feat : 新功能
-   fix : 修复bug
-   docs : 文档改变
-   style : 代码格式改变
-   refactor : 某个已有功能重构
-   perf : 性能优化
-   test : 增加测试
-   build : 改变了build工具 如 grunt换成了 npm
-   revert : 撤销上一次的 commit
-   chore : 构建过程或辅助工具的变动

( 2 ) scope（可选） : 用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同。

( 3 ) subject（必须） : commit 的简短描述，不超过50个字符。  
commitizen 是一个撰写合格 Commit message 的工具，  
遵循 Angular 的提交规范。

### 制定适合我们的 git commit 提交规范

#### 格式

`type: description`

#### 1\. type 类型

type 是 commit 的类别，只允许如下几种标识：

-   fix: 修复bug
-   add: 新功能
-   update: 更新
-   style : 代码格式改变
-   test: 增加测试代码
-   revert: 撤销上一次的commit
-   build: 构建工具或构建过程等的变动，如：gulp 换成了 webpack，webpack 升级等

#### 2\. description

description 是对本次提交的简短描述。

不超过50个字符。

推荐以动词开头，如： 设置、修改、增加、删减、撤销等
