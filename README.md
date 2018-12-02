# SendFileTree
Zero Copy零拷贝技术研究


网络文件传输---传统非零拷贝技术

![](https://i.imgur.com/dfoefdf.png)

网络文件传输---零拷贝技术

![](https://i.imgur.com/x0c2AbN.png)

<pre>
传统方式：
       read(file, tmp_buf, len);      
       write(socket, tmp_buf, len);

       1、调用read函数，文件数据被copy到内核缓冲区 
       2、read函数返回，文件数据从内核缓冲区copy到用户缓冲区 
       3、write函数调用，将文件数据从用户缓冲区copy到内核与socket相关的缓冲区。 
       4、数据从socket缓冲区copy到相关协议引擎。
</pre>

<pre>
零拷贝方式：
       sendfile(socket, file, len);
 
       1、sendfile系统调用，文件数据被copy至内核缓冲区 
       2、再从内核缓冲区copy至内核中socket相关的缓冲区 
       3、最后再socket相关的缓冲区copy到协议引擎
</pre> 

<pre>
应用场景：
       Nginx：
            设置 sendfile on
</pre>