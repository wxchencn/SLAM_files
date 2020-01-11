# Unit2

## 1.熟悉 Eigen 矩阵运算
设线性方程组 $Ax = b$，在 $A$ 为方阵的前提下，请回答一下问题：

1. **在什么条件下，$x$ 有解且唯一？**
$$r(A) = r(A,b) = n$$

2. **高斯消元法的原理是什么？**
将系数矩阵和右侧值组合成增广矩阵，通过初等行变换将增广矩阵化为行阶梯矩阵，然后通过回代求解线性方程组的解。
[高斯消元](https://blog.csdn.net/pengwill97/article/details/77200372)

3. **$QR$ 分解的原理是什么？**
QR分解通常用来求解线性最小二乘问题，把矩阵分解为一个正交矩阵和一个上三角矩阵。
即 $A_{m\times n} = Q_{m\times m}R_{m\times n}$ ，其中 $Q$ 为正交矩阵 $Q^TQ = I$
4. **$Cholesky$ 分解的原理是什么？**
$Cholesky$ 分解法又叫平方根法，是求解对称正定线性方程组常用的方法。
**定理：** 若 $A\in R^{n\times n}$ 对称正定，则存在一个对角元为正数的下三角矩阵 $L\in R^{n\times n}$ ，使得 $A = LL^T$ 成立。
若求解线性方程组 $Ax = b$ ，其中 $A$ 为对称正定矩阵，那么 $x$ 可通过下面步骤求解：
   - 求 $A$ 的 $Cholesky$ 分解，得到 $A=LL^T$
   - 求解$Ly=b$，得到$y$
   - 求解$L^Tx=y$，得到$x$

    矩阵分解内容参考：[【数值计算】LU分解、LUP分解、Cholesky分解](https://zhuanlan.zhihu.com/p/84210687)

5. **编程实现 $A$ 为 $100\times 100$ 随机矩阵时，用 $QR$ 和 $Cholesky$ 分解求 $x$ 的程序。**
   
    **useEigen.cpp**
    ```cpp
    #include <iostream>
    #include <Eigen/Core>
    #include <Eigen/Dense>
    #include <ctime>

    #define MATRIX_SIZE 100

    int main(){
        Eigen::Matrix<double,Eigen::Dynamic,Eigen::Dynamic> A;//声明动态矩阵A
        A = Eigen::MatrixXd::Random(MATRIX_SIZE, MATRIX_SIZE);
        A = A.transpose() * A;//生成对称矩阵
        std::cout<<"Matrix_A:"<<std::endl;
        std::cout<<A<<std::endl;
        Eigen::Matrix<double,Eigen::Dynamic,1> B;
        B = Eigen::MatrixXd::Random(MATRIX_SIZE, 1);
        Eigen::Matrix<double, Eigen::Dynamic, 1> x;
        clock_t time_stt = clock();
        //QR分解
        x = A.colPivHouseholderQr().solve(B);
        std::cout << "QR time use:" << 1000*(clock()-time_stt)/(double) CLOCKS_PER_SEC << "ms" << std::endl;
        std::cout << "QR result" << std::endl;
        std::cout << x << std::endl;
        //LLT分解 Cholesky
        time_stt = clock();
        x = A.llt().solve(B);
        std::cout << "LLT time use:" << 1000*(clock()-time_stt)/(double) CLOCKS_PER_SEC << "ms" << std::endl;
        std::cout << "LLT result" << std::endl;
        std::cout << x << std::endl;
        return 0;
    }
    ```
    **CMakeLists.txt**
    ```cpp
    cmake_minimum_required(VERSION 2.8)
    project(useEigen)
    set(CMAKE_BUILD_TYPE "Release")
 
    include_directories("/usr/include/eigen3")
    add_executable(useEigen useEigen.cpp)
    ```
## 2.几何运算练习
**设有小萝卜一号和二号位于世界坐标系中。小萝卜一号的位姿为：$q_1 = [0.55,0.3,0.2,0.2], t_1 = [0.7,1.1,0.2]^T (q的第一项为实部)$。这里的 $q$ 和 $t$ 表达的是 $T_{cw}$ ，也就是世界到相机的的变换关系。小萝卜二号的位姿为$q_2 = [-0.1,0.3,-0.7,0.2],t_2 = [-0.1,0.4,0.8]^T$。现在，小萝卜一号看到某个点在自身的坐标系下，坐标为$p_1 = [0.5,-0.1,0.2]^T$，求该向量在小萝卜二号坐标系下的坐标。**

解答：设点 $p$ 在世界坐标系下的坐标为 $p_w$ ，则：
\[p_1 = q_1p_wq_1^{-1} + t_1\\ p_2 = q_2p_wq_2^{-1} + t_2\\ \]
由此求得 $p_2$。
### 代码实现：

**geometry.cpp**
```cpp
#include<iostream>
#include<cmath>
#include<Eigen/Core>
#include<Eigen/Dense>
#include<Eigen/Geometry>

int main(){
    Eigen::Vector3d p1, t1, t2;
    p1 << 0.5, -0.1, 0.2;
    t1 << 0.7, 1.1, 0.2;
    t2 << -0.1, 0.4, 0.8;

    Eigen::Quaterniond q1 = Eigen::Quaterniond(0.55, 0.3, 0.2, 0.2).normalized();
    // Eigen::Quaterniond初始化顺序为(w, x, y, z).实际存储顺序为(x, y, z, w)
    Eigen::Quaterniond q1_c = q1.conjugate();
    // conjugate()为q1的共轭，因为需要相机到世界坐标系的旋转
    std::cout<< "q1_c:"<< q1_c.coeffs().transpose()<<std::endl;
    //transpose()转置为行向量显示
    Eigen::Quaterniond q2 = Eigen::Quaterniond(-0.1, 0.3, -0.7, 0.2).normalized();
    std::cout<< "q2:"<< q2.coeffs().transpose()<<std::endl;
    Eigen::Vector3d pw = q1_c*(p1 - t1);
    Eigen::Vector3d p2 = q2*pw + t2;
    std::cout<<"p2:"<< p2.transpose() <<std::endl;
    return 0;
}
```
**CMakeLists.txt**
```cpp
cmake_minimum_required(VERSION 2.8)
project(geometry)
set(CMAKE_BUILD_TYPE "Release")

include_directories("/usr/include/eigen3")
add_executable(geometry geometry.cpp)
```
## 3.旋转的表达
证明：
1. **设有旋转矩阵 $R$ ，证明 $R^TR = I$ 且 $detR = +1$。**
   即证明 $R^T = R^{-1}$
   参考：[旋转矩阵的性质](https://www.cnblogs.com/caster99/p/4703033.html)
2. **设有四元数 $q$，我们把虚部记为 $\varepsilon$ ，实部记为 $\eta$ ，那么 $q = (\varepsilon,\eta)$。请说明 $\varepsilon$ 和 $\eta$ 的维度。**
   四元数的实部 $\eta$ 维度为一维，虚部 $\varepsilon$ 维度为三维。

3. **定义运算 $+$ 和 $\oplus$ 为：**
   $$q^+ = \begin{bmatrix} {\eta 1 - \varepsilon^\times}&\varepsilon \\\\ {-\varepsilon^T}&\eta \end{bmatrix}, q^{\oplus} = \begin{bmatrix} {\eta 1 + \varepsilon^\times}&\varepsilon \\\\ {-\varepsilon^T}&\eta \end{bmatrix},\tag{1}$$
   **请证明对任意单位四元数 $q_1,q_2$，四元数乘法可写成矩阵乘法：**
   $$q_1\cdot q_2 = q^+_1q_2 \tag{2}$$
   **或者**
   $$q_1\cdot q_2 = q_2^{\oplus} q_1 \tag{3}$$
   证明：根据公式 $q_aq_b = [\eta_a\eta_b - \varepsilon_a^T\varepsilon_b, \eta_a\varepsilon_b + \eta_b\varepsilon_a + \varepsilon_a \times \varepsilon_b]$ 容易得证。
## 4.罗德里格斯公式的证明
**罗德里格斯公式描述了从旋转向量到旋转矩阵的转换关系。设旋转向量长度为 $\theta$ ，方向为 $n$ ，那么旋转矩阵 $R$ 为：**
$$R = cos{\theta I} - (1 - cos\theta)nn^T + sin{\theta n^\wedge}\tag{4}$$
**请证明此式。**
证明：
![rodeigues-formula](/images/Rodeigues-formula.png)
![rodeigues](/images/Rodrigues.png)

## 5.四元数运算性质的验证
