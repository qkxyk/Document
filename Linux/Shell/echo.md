### Shell echo命令
Shell的echo命令用于字符串的输出，其格式为:  
```Shell
echo string
```
1. 显示普通字符串
   ```Shell
   echo "It is a test"
   #这里双引号可以省略，以下命令同上
   echo It is a test
   ```
2. 显示转义字符  
   ```Shell
   echo "\"It is test \""
   #输出： "It is test"
   ```  
3. 显示变量  
   read命令从标准输入中读取一行，并把输入行的每个字段的值指定给shell变量。  
   ```Shell
   read name
   echo "$name It is test"
   ```
   执行shell，并输入数据后回车即可看到结果。
4. 显示换行 
   ```shell
   echo -e "OK! \n" # -e 开启转义 
   echo "It is a test"
   ```  
5. 显示不换行 
   ```Shell
   echo -e "OK! \c" # -e开始转义， \c不换行
   echo "It is a test"
   ```
6. 显示结果定向至文件  
   ```shell
   echo "It is a test" > myfile
   ```
7. 原样输出字符串，不进行转义或取变量(用单引号)  
   ```shell
   echo '$name\"'
   #输出 $name\"
   ```
8. 显示命令执行结果  
   ```shell
   echo `date`
   ```
   注：这里时反引号不是单引号，结果显示当前日期。





