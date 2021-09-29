## 一、DNS是什么？
DNS （Domain Name System 的缩写）的作用非常简单，就是根据域名查出IP地址。你可以把它想象成一本巨大的电话本。
比如我们使用的www.baidu.com ,它的ip是110.242.68.3
```shell
~/workspace  ping www.baidu.com
PING www.a.shifen.com (110.242.68.3): 56 data bytes
64 bytes from 110.242.68.3: icmp_seq=0 ttl=45 time=14.169 ms
64 bytes from 110.242.68.3: icmp_seq=1 ttl=45 time=28.007 ms
64 bytes from 110.242.68.3: icmp_seq=2 ttl=45 time=72.009 ms
```

