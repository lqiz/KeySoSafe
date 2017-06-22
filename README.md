# KeySoSafe  
本工程使用最简单的 cmake
将秘钥放入SO，通过包名和签名的比对，以防止可以防止so库被其他人二次打包


#### 使用方法
1. src/main/cpp/native-lib.cpp 里的 const char *app_signature 需要设置为
app 的签名，具体方法见源文件注释。
2. 当前 sign_sha1_verify 必定返回false，设置后返回true，既验证正确。
3. 当更改包结构失衡，要注意 ApiKeyGeneractor 里 keyFromJNI 对应cpp文件里的
函数名，需要重新生成。

#### 安全说明
以上只是最简单的措施，只是增加了破解代价，并非安全
1. 通过IDA进行反编译so进行破解。(对应：so加固)
2. 可以修改了这些java引用路径，欺骗so，让他获取到正确的签名。(对应：apk加固)
3. IDA动态分析。（对应：反dump和反调试）