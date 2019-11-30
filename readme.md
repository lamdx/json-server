# json-server

## 下载安装

```shell
# 全局安装json-server
npm install -g json-server
```

```shell
# 查看json-serve 版本
json-server -v
```

## 创建 json 数据

创建任意一个文件夹并进入到该文件夹里面，执行代码：

```shell
# package.json文件初始化
npm init -y
# 如果没有db.json 就创建db.json
json-server --watch db.json
```

## json-server 修改端口

json-server 默认是 3000 端口，我们也可以自己指定端口，指令如下：

```shell
json-server db.json --port 3004
```

## 简写命令

如果你很懒，觉得启动服务的这段代码有点长，可以把配置信息写在 package.json 文件里面：

```json
{
  "scripts": {
    "mock": "json-server db.json --port 3004"
  }
}
```

之后启动服务，只需要执行如下指令就可以了：

```shell
npm run mock
```

## 常规获取数据

### 过滤获取 Filter

http://localhost:3000/fruits/1 可以得到指定 id 为 1 的水果(对象)

我们也可以通过水果名称，或者是价格来获取数据：

http://localhost:3000/fruits?name=orange

```json
[
  {
    "id": 2,
    "name": "orange",
    "price": "8.88"
  }
]
```

也可以指定多个条件，用&符号连接：

http://localhost:3000/fruits?name=orange&price=8.88

你甚至还可以使用对象取属性值 obj.key 的方式：

http://localhost:3000/users?name.nickname=dachui

### 分页

分页采用`_page`来设置页码，`_limit`来控制每页显示条数。如果没有指定`_limit`，默认每页显示 10 条

http://localhost:3000/fruits?_page=2&_limit=2

### 排序 Sort

排序采用`_sort`来指定要排序的字段，`_order`来指定排序是正排序还是逆排序(asc | desc ，默认是 asc)

http://localhost:3000/fruits?_sort=id&_order=desc

### 取符合某个范围 Operators

采用 `_gte` `_lte` 来设置一个取值范围(range)：

http://localhost:3000/fruits?id_gte=4&id_lte=6

采用`_ne` 来设置不包含某个值：

http://localhost:3000/fruits?id_ne=1

### 全文搜索 Full-text search

采用 q 来设置搜索内容：

http://localhost:3000/fruits?q=oran

```json
[
  {
    "id": 6,
    "name": "orange",
    "price": "8.88"
  }
]
```

## json-server 修改默认路由

创建 routes.json 文件

```json
{
  "/details\\?lid=:b": "/details/:b",
  "/products\\?kws=:a": "/products?title_like=:a"
}
```

```shell
json-server ./doc/db.json --routes ./doc/routes.json
```
