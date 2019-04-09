# react

## 1.用npm安装react时报错

## ` Refusing to install react as a dependency of itself`

##### 不能把项目取名为 react，项目的 package.json 里面 `name` 的值不能是 `react`，也不能是你项目其他依赖包的名字，也就是和依赖包不能重名

## 2.用npm安装包总是出现的警告

`npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@^1.0.0 `

**fsevent是mac osx系统的，在win或者Linux下使用了 所以会有警告，忽略即可**

## 3.用npm安装包报错

nmp安装问题总是报这个错，但是其实是安装成功的

```
npm warn package.json @1.0.0 no repository field.
```

看字面意思大概是package.json里缺少repository字段，也就是说缺少项目的仓库字段

```
{
    ...
    "repository": {
        "type": "git",
        "url": "http://baidu.com"
    },
    ...
}
```

但作为测试项目或者练习用，只需在package.json里面做如下配置即可:

```
{
    ...
    "private": true,
    ...
}

```

以这种方式把项目声明为私有。

## 4.用npm安装包报错

package.json

```
{
    ...
    "repository": {
        "type": "git",
        "url": "http://baidu.com", // 此处多加了逗号，就会报错，去掉
    },
    ...
}
```

