# https通信过程
1. 客户端发送一个请求去服务器端
2. 服务器发送了一个SSL证书给客户端，SSL 证书中包含的具体内容有：（1）证书的发布机构CA （2）证书的有效期 （3）公钥 （4）证书所有者 （5）签名（6）hash算法
3. 客户端在接受到服务端发来的SSL证书时，会对证书的真伪进行校验，以浏览器为例说明如下：
（1）首先浏览器读取证书中的证书所有者、有效期等信息进行一一校验
（2）浏览器开始查找操作系统中已内置的受信任的证书发布机构CA，与服务器发来的证书中的颁发者CA比对，用于校验证书是否为合法机构颁发
（3）如果找不到，浏览器就会报错，说明服务器发来的证书是不可信任的。
（4）如果找到，那么浏览器就会从操作系统中取出 颁发者CA 的公钥，然后对服务器发来的证书里面的签名进行解密
（5）浏览器使用相同的hash算法计算出服务器发来的证书的hash值，将这个计算的hash值与证书中签名做对比
（6）对比结果一致，则证明服务器发来的证书合法，没有被冒充
（7）此时浏览器就可以读取证书中的公钥，用于后续加密了
4. 验证服务器的身份后，客户端生成一个对称加密算法和密钥，用于后面的通信的加密和解密。这个对称加密算法和密钥，客户会用公钥加密后发送给服务器，别人截获了也没用，因为只有“服务器”手中有可以解密的私钥。
   这样，后面服务器和客户端就都可以用对称加密算法来加密和解密通信内容了
