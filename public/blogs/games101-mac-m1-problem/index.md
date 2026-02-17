## 作业 0

在 mac 上安装些许困难，最终参考了稀土掘金的教程解决了。

> [https://juejin.cn/post/7144284278023684133#heading-10](https://juejin.cn/post/7144284278023684133#heading-10)。

按照该步骤：
- 安装 `homebrew`、`gcc`、`cmake` 即可。这里我之前都装过了。
- 用 `homebrew` 安装 `Eigen`。
- 编译过程注意 `eigen` 库安装的位置可能是和作者不一样的，比如我就是：`/opt/homebrew/Cellar/eigen/5.0.1`。
- `CMakeLists.txt` 也报了错，原因是 `CMake` 的版本太老了，问了 Gemini 这样改成功跑通了：

```
cmake_minimum_required (VERSION 2.8.11...3.27)
project (homework0)

find_package(Eigen3 REQUIRED)
include_directories("/opt/homebrew/Cellar/eigen/5.0.1/include")

add_executable (main main.cpp)
```

> `2.8.11...3.27` 表示兼容前面的版本，这里的 `include_directories("/opt/homebrew/Cellar/eigen/5.0.1/include")` 改成自己的位置，可以自己找一下。

最后按照作业中的要求正常编译就好了：

```sh
mkdir build
cd build
cmake ..
make
./main # 运行程序

# 下面是输出的结果（表明程序跑通了🎉(*^▽^*)）
Example of cpp 
1
0.5
1.41421
3.14159
0.5
Example of vector 
Example of output 
1
2
3
Example of add 
2
2
3
Example of scalar multiply 
3
6
9
2
4
6
Example of matrix 
Example of output 
1 2 3
4 5 6
7 8 9
```