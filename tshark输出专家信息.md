# Tshark输出专家信息
tshark -- A terminal orentied version of Wireshark

## 1. 显示专家信息
在tshark中显示专家信息，示例命令如下：
```
tshark -r file.pcap -Y '_ws.expert.severity == "Warning"' -T fields -e frame.number -e _ws.expert
tshark -r file.pcap -Y '_ws.expert.severity == "Warning"' -T fields -E separator=, -E quote=d -E header=y -e frame.number -e _ws.expert

tshark -r 1111.pcapng -Y '_ws.expert.severity == "Warning" || _ws.expert.severity=="Note" || _ws.expert.severity=="Error"' -T fields -E separator=, -E quote=d -E header=y -e frame.number -e _ws.expert

输出所有Note及以上级别的专家信息
tshark -r 1111.pcapng -Y '_ws.expert.severity == "Warning" || _ws.expert.severity=="Note" || _ws.expert.severity=="Error"' -T fields -E separator=, -E quote=d -E header=y -e frame.number -e frame.time_epoch -e ip.src -e ip.dst -e tcp.srcport -e tcp.dstport  -e frame.len -e _ws.expert
```
-r: 输入的pcap或pcapng文件
-Y: 过滤器，display filter,
-T: 设置输出的格式
-e: 显示的字段field
-E: 设置field字段的输出格式
Wireshark中的Expert信息是由wireshark分析出来的一种异常(anomaly)，作为诊断问题的一种提示，十分有用。 https://www.wireshark.org/docs/wsug_html_chunked/ChAdvExpert.html

## 2. 过滤TCP流到Python代码中进行分析
```
/usr/bin/tshark -l -n -T pdml -Y tcp -r /home/tanxiaobing/Pcap/1111.pcapng
```
-l： 及时刷新标准输出，常用在以管道形式与其它程序连接时的处理，以提高下游程序的处理效率
-n： 关闭域名解析，不对IP进行域名解析，直接显示IP地址
-T： 设置输出格式。 pdml表示以xml格式输出。

## 3. 如何找到所有合法的fields
Wireshark的强大特征之一就是拥有大量的过滤器。这些过滤器都是基于field构建的。 Wireshark-3.0.3版本包含3000种协议，各类field总数超过242000！如何找到自己想要的fields呢，怎么知道有哪有fields可供使用呢0？通常有四种方法：
- [查看文档](https://www.wireshark.org/docs/dfref/) 
- 从Wireshark界面的Expression按钮中查找field
- 使用过滤窗口的补全功能
- tshark -G fields

## 4. Wireshark中的Info列与由字段 _ws.col.Info 表示
```
tshark -r traffic.pcap -T fields -E separator=, -e frame.number -e frame.time_epoch -e ip.src -e ip.dst -e tcp.srcport -e tcp.dstport  -e frame.len -e tcp.flags -e _ws.col.Protocol -e _ws.col.Info -E header=y -E quote=d -E occurrence=f
```
