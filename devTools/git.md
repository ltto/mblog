#git如何使用
>首先git 协议是基于openssh的 所以需要使用者有自己的sshkey
+ **生成sshkey**
command:
`ssh keygen -t rsa -C "you email"`
默认会生成到自己的用户目录下面的`.ssh`目录