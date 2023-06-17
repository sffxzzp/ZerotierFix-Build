ZerotierFix-Build
======

一个使用 Github Actions 的 [ZerotierFix](https://github.com/kaaass/ZerotierFix) 构建，没有签名，需要自己签名或者手机有核心破解。

~~根据 [ZerotierFix#31](https://github.com/kaaass/ZerotierFix/issues/31) 的脚本，实现自动编译 ZeroTier Core 以及更新 ZerotierFix 中的 SDK。~~

现已改用 CMake 编译，使用 NDK-Build 编译，可参考[此处](https://github.com/sffxzzp/ZerotierFix-Build#%E4%BD%BF%E7%94%A8-ndk-build-%E7%BC%96%E8%AF%91%E7%9A%84%E5%8F%82%E8%80%83)。

点击此处 [下载](https://nightly.ore-imo.tk/ZerotierFix-Build)。

使用 CMake 编译 libZeroTierOneJNI.so 的步骤
------

想了半天，应该还是因为官方库里 CMakeLists.txt 的问题，根据 Android.mk 以及编译时候的报错信息对文件进行了修改。

当前可以正常编译通过，但并未进行过测试。

编译步骤如下：
1. 首先 cd 至 ZeroTierOne/java

2. 其次执行下面的代码

``` shell
cmake -DCMAKE_TOOLCHAIN_FILE=$NDKHOME/build/cmake/android.toolchain.cmake -DANDROID_ABI=$ABI -DANDROID_PLATFORM=android-24
make
```

其中 `$NDKHOME` 是 NDK 的安装目录；`$ABI` 是编译的安卓架构，有 `armeabi-v7a`、`arm64-v8a`、`x86` 和 `x86_64` 可选，但理论上应当全部编译。

`make` 后 `libZeroTierOneJNI.so` 生成在 `ZeroTierOne/java`，之后编译环境可能需要清理以进行下一次编译。

以上，另附上资料参考：https://developer.android.google.cn/ndk/guides/cmake?hl=zh-cn

使用 NDK-Build 编译的参考
------
[编译 dev 分支](https://github.com/sffxzzp/ZerotierFix-Build/tree/b8b7b28d26f1ada9e272d43dfb7283ccc231fcdd)

[编译 main 分支](https://github.com/sffxzzp/ZerotierFix-Build/tree/94add5f4cc6f0fb8c1237fa9b822708848d9221c)
