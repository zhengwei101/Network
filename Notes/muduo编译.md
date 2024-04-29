# muduo 编译

## 1. 下载muduo

```bash
git clone https://github.com/chenshuo/muduo.git
```

## 2. 我这里使用cpp17分支的进行编译

```bash
cd muduo
git checkout cpp17
```

## 3. 编译并安装

```bash
./build.sh install
```
若提示权限不够，先使用chmod命令对shell脚本赋予权限，再执行
`chmod 777 ./build.sh`

## 4. 修改`ttcp_asio_async.cc`

```c++
  TtcpServerConnection(const tcp::socket::executor_type& executor)
```

## 5. 编译安装后，会在muduo同级目录，生成release-cpp17和release-install-cpp17文件夹

```bash
# 拷贝release-install-cpp17中include和lib目录中的文件到系统目录
cd build/release-install-cpp17/
cd include/
sudo cp -r muduo /usr/include/

cd build/release-install-cpp17/
cd lib/
sudo cp -r * /usr/local/lib/

```

## 6. 编译并运行示例代码

```bash
cd muduo/examples/simple/echo/
g++ -o echo echo.cc main.cc -lmuduo_net -lmuduo_base -lpthread -std=c++17

# 运行echo程序
./echo

# 另开一个终端，与echo server 连接
echo "hello world" | nc localhost 2007

```