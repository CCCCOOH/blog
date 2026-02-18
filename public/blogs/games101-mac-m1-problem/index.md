## 作业 0

> 更新于 2026 年 1 月。

在 `M1 Mac` 上安装些许困难，最终参考了稀土掘金的教程解决了，抛弃了虚拟机的方案，直接在本机部署环境一劳永逸，还算快的。

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

### 作业代码实现

```c++
#include<cmath>
#include<eigen3/Eigen/Core>
#include<eigen3/Eigen/Dense>
#include<iostream>

int main(){

    // Basic Example of cpp
    std::cout << "Example of cpp \n";
    float a = 1.0, b = 2.0;
    std::cout << a << std::endl;
    std::cout << a/b << std::endl;
    std::cout << std::sqrt(b) << std::endl;
    std::cout << std::acos(-1) << std::endl;
    std::cout << std::sin(30.0/180.0*acos(-1)) << std::endl;
    // 30/180 * pib = 1/6 pi

    // Example of vector
    std::cout << "Example of vector \n";
    // vector definition
    Eigen::Vector3f v(1.0f,2.0f,3.0f);
    Eigen::Vector3f w(1.0f,0.0f,0.0f);
    // vector output
    std::cout << "Example of output \n";
    std::cout << v << std::endl;
    // vector add
    std::cout << "Example of add \n";
    std::cout << v + w << std::endl;
    // vector scalar multiply
    std::cout << "Example of scalar multiply \n";
    std::cout << v * 3.0f << std::endl;
    std::cout << 2.0f * v << std::endl;

    // Example of matrix
    std::cout << "Example of matrix \n";
    // matrix definition
    Eigen::Matrix3f i,j;
    i << 1.0, 2.0, 3.0, 4.0, 5.0, 6.0, 7.0, 8.0, 9.0;
    j << 2.0, 3.0, 1.0, 4.0, 6.0, 5.0, 9.0, 7.0, 8.0;
    // matrix output
    std::cout << "Example of output \n";
    std::cout << i << std::endl;
    // matrix add i + j
    std::cout << "Example of matrix add \n";
    std::cout << i + j << std::endl;
    // matrix scalar multiply i * 2.0
    std::cout << "Example of matrix scalar multiply i * 2.0" << std::endl;
    std::cout << i * 2.0f << std::endl;
    // matrix multiply i * j
    std::cout << "Example of matrix multiply multiply  i * j" << std::endl;
    std::cout << i * j << std::endl;
    // matrix multiply vector i * v
    std::cout << "Example of matrix multiply vector i * v" << std::endl;
    std::cout << i * v << std::endl;

    std::cout << "Homework start output" << std::endl;
    Eigen::Vector3f P(2.0f, 1.0f, 1.0f);
    Eigen::Matrix3f R, T;
    float theta = 1.0/4.0 * acos(-1);
    // std::cout << "theta: " << theta << std::endl;
    R << cos(theta), -sin(theta), 0.0, cos(theta), sin(theta), 0.0, 0.0, 0.0, 1.0;
    T << 0.0, 0.0, 1.0, 0.0, 0.0, 2.0, 0.0, 0.0, 1.0;
    std::cout << "旋转变换后 R*P:\n" << R * P << std::endl; 
    std::cout << "平移变换后 T*R*P:\n" << T * R * P << std::endl;
    return 0;
}
```

作业最后算出的结果是：
$$
\begin{bmatrix}
1 \\
2 \\
1
\end{bmatrix}
$$

> 手算一下就可以很简单地验证。


## 作业 1

做这个作业也是一上来就遇到报错了，发现是因为没有安装 `opencv@2` 的原因，但发现 `opencv2` 已经停止维护了😅，不过根据我上一次的经验，我还是跑通了！

安装好 `opencv` 后需要修改 `main.cpp` 中的引入代码，因为现在已经是 `opencv4` 了：

```c++
#include <opencv4/opencv2/opencv.hpp>
```

> 这里建议亲自根据 `brew info opencv` 去调查一下文件目录再写入，只需要保证是从 `/include` 这个位置开始就对了，比如我这里实际目录的结构是 `/opt/homebrew/Cellar/eigen/5.0.1/include/opencv4/opencv2/opencv.hpp`。

首先更改 `CMakeLists.txt`：

```sh
cmake_minimum_required (VERSION 2.8.11...3.27)
project (homework0)

find_package(OpenCV REQUIRED)

message(STATUS "Eigen3 include dirs: ${EIGEN3_INCLUDE_DIRS}")
message(STATUS "OpenCV include dirs: ${OpenCV_INCLUDE_DIRS}")
set(CMAKE_CXX_STANDARD 17)

include_directories("/opt/homebrew/Cellar/eigen/5.0.1/include")
include_directories("/opt/homebrew/Cellar/opencv/4.13.0_3/include")


add_executable(Rasterizer main.cpp rasterizer.hpp rasterizer.cpp Triangle.hpp Triangle.cpp)
target_include_directories(Rasterizer PRIVATE 
    ${EIGEN3_INCLUDE_DIRS} 
    ${OpenCV_INCLUDE_DIRS}
)
target_link_libraries(Rasterizer ${OpenCV_LIBRARIES})
```

然后在 `代码框架` 目录进行编译即可：

```sh
mkdir build && cd build && cmake .. && make
```

在 `/build`  下运行：

```sh
./Rasterizer
```

紧接着会在终端中输出，并打开一个窗口！

> 终于可以开始写作业了，太棒了！🚀

