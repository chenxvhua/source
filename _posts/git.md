---
title: 关于git使用介绍
categories: [other]
---
# 关于git使用介绍

## git怎么配置秘钥
 
      在终端中敲下面的命令，第一步会生成一对私钥和公钥，分别存在 ~/.ssh/id_rsa和~/.ssh/id_rsa.pub中。第二步查看公钥字符串。
      ssh-keygen -t rsa -C "$your_email" 
      cat ~/.ssh/id_rsa.pub 

    
## gitlab怎么配置
       在面板上依次点击Profile Settings –> SSH Keys –> Add SSH Keys。然后把上一步中的id_rsa.pub中的内容拷贝出来粘贴到输入框中，保存
    




