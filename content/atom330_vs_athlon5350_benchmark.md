Title: 2008年と2015年に組んだ省電力サーバーのベンチマーク比較
Date: 2015-05-25 20:44
Author: waura
Category: サーバー管理
Tags: unixbench, ベンチマーク, 省電力サーバー, 自宅サーバー
Slug: atom330_vs_athlon5350_benchmark
Status: published

はじめに
--------

サーバーを新しく組んだので、ベンチマークの比較をしてみます。  
比較対象サーバーの構成の比較は下記のとおりです。

|| 2008年 | 2015年 |  
|:---:|:---|:---|  
|CPU|Intel Atom330|AMD Athlon5350|  
|メモリ|DDR2-800 2GB|DDR3-1600 16GB|  

 

ベンチマークソフトは[unixbench](https://code.google.com/p/byte-unixbench/)を使用します。

 

Atom330とAthlon5350のスペック比較
---------------------------------

|| Atom330 | Athlon5350 |  
|:---|---:|---:|  
|周波数|1.6GHz|2.05GHz|  
|L1 cache|64 KB (code) / 48 KB (data)|128 KB (code) / 128 KB
(data)|  
|L2 cache|1024KB|2048KB|  
|TDP|8W|25W|  
|実Core数|2|4|  

 

Atom330とAthlon 5350のベンチマーク比較
--------------------------------------

Atom330とAthlon5350のベンチマークの比較結果です。

4 parallel processの結果を比較しています。

|Test| 2007年(Atom330) | 2015年(Athlon5350) | 伸び率(2015年のスコア/ 2008年のスコア)|  
|:---|---:|---:| ---:|  
|Dhrystone 2 using register variables|1362.9|4958.9|3.64  
|Double-Precision Whetstone|571.8| 1846.4|3.23|  
|Execl Throughput|377.4| 2081.6|5.52|  
|File Copy 1024 bufsize 2000 maxblocks|305.4| 1832.6|6.00  
|File Copy 256 bufsize 500 maxblocks|196.0 | 1384.9|7.07  
|File Copy 4096 bufsize 8000 maxblocks|573.1 | 3170.0|5.53|  
|Pipe Throughput|434.5| 1910.3|4.40|  
|Pipe-based Context Switching|224.1 | 918.6|4.10|  
|Process Creation|361.8| 1986.7|5.49|  
|Shell Scripts (1 concurrent)|760.3| 1785.4|2.35|  
|Shell Scripts (8 concurrent)|700.2| 2088.1|2.98|  
|System Call Overhead|1052.5 | 2531.4|2.41  
|System Benchmarks Index Score:|  491.6| 2035.0|4.14|

 

すべての項目でスコアが伸びてます。

特にFile Copyの伸びが大きいです。

File Copy
1024...のテスト内容は、2MByteのファイルを1024Byteごとに処理します。

File Copy 256...は、500KByteのファイルを256Byteごと、File
Copy4096...は、8MByteのファイルを4096Byteごとに処理します。

 

スコアの伸びが大きいのは、下記の要因が大きそうです。

・Atom330が物理コア2個に対して、Athlon5350が4個

・Atom330の動作クロック1.6GHzに対して、Athlon5350が2.05GHz

 

2008年と2015年に組んだときにかかったお金はほぼ同額です。

Atom330のボードとAthlon5350+マザーボードはどちらも1万円程度で購入しました。

7年も経つと同じ金額でもここまで全体的にスペックが底上げされたサーバーが組めるようになるようです。

 

 

参考
----

### Atom330

#### 1 parallel process

|Test| Score| Unit| Time| Iters.| Baseline| Index|  
|:---|---:|:---|---:|---:|---:|---:|
|Dhrystone 2 using register variables| 5881155.3| lps| 10.0 s| 7|116700.0| 504.0|  
|Double-Precision Whetstone| 872.9| MWIPS| 9.8 s| 7| 55.0|158.7|  
|Execl Throughput| 657.2| lps| 29.6 s| 2| 43.0| 152.8|  
|File Copy 1024 bufsize 2000 maxblocks| 118195.2| KBps| 30.0 s| 2|3960.0| 298.5|  
|File Copy 256 bufsize 500 maxblocks| 33060.5| KBps| 30.0 s| 2|1655.0| 199.8|  
|File Copy 4096 bufsize 8000 maxblocks| 317990.6| KBps| 30.0 s| 2|5800.0| 548.3|  
|Pipe Throughput| 404343.1| lps| 10.0 s| 7| 12440.0| 325.0|  
|Pipe-based Context Switching| 21144.8| lps| 10.0 s| 7| 4000.0|52.9|  
|Process Creation| 1800.5| lps| 30.0 s| 2| 126.0| 142.9|  
|Shell Scripts (1 concurrent)| 1743.6| lpm| 60.0 s| 2| 42.4|411.2|  
|Shell Scripts (8 concurrent)| 406.3| lpm| 60.1 s| 2| 6.0|677.1|  
|System Call Overhead| 897649.1| lps| 10.0 s| 7| 15000.0|598.4|  
|System Benchmarks Index Score:| | | | | | 271.9|  

#### 4 parallel processes

|Test| Score| Unit| Time| Iters.| Baseline| Index|  
|:---|---:|:---|---:|---:|---:|---:|
|Dhrystone 2 using register variables| 15904701.2| lps| 10.0 s| 7|116700.0| 1362.9|  
|Double-Precision Whetstone| 3144.8| MWIPS| 9.8 s| 7| 55.0|571.8|  
|Execl Throughput| 1622.7| lps| 29.6 s| 2| 43.0| 377.4|  
|File Copy 1024 bufsize 2000 maxblocks| 120953.8| KBps| 30.0 s| 2|3960.0| 305.4|  
|File Copy 256 bufsize 500 maxblocks| 32443.7| KBps| 30.0 s| 2|1655.0| 196.0|  
|File Copy 4096 bufsize 8000 maxblocks| 332388.0| KBps| 30.0 s| 2|5800.0| 573.1|  
|Pipe Throughput| 540570.0| lps| 10.0 s| 7| 12440.0| 434.5|  
|Pipe-based Context Switching| 89659.6| lps| 10.0 s| 7| 4000.0|224.1|  
|Process Creation| 4558.4| lps| 30.0 s| 2| 126.0| 361.8|  
|Shell Scripts (1 concurrent)| 3223.8| lpm| 60.0 s| 2| 42.4|760.3|  
|Shell Scripts (8 concurrent)| 420.1| lpm| 60.4 s| 2| 6.0|700.2|  
|System Call Overhead| 1578750.6| lps| 10.0 s| 7| 15000.0|1052.5|  
|System Benchmarks Index Score:| | | | | | 491.6|  

### Athlon 5350

#### 1 parallel processes

|Test| Score| Unit| Time| Iters.| Baseline| Index|  
|:---|---:|:---|---:|---:|---:|---:|  
|Dhrystone 2 using register variables| 14343277.6| lps| 10.0 s| 7|116700.0| 1229.1|  
|Double-Precision Whetstone| 2549.9| MWIPS| 9.6 s| 7| 55.0|463.6|  
|Execl Throughput| 861.3| lps| 29.9 s| 2| 43.0| 200.3|  
|File Copy 1024 bufsize 2000 maxblocks| 347747.1| KBps| 30.0 s| 2|3960.0| 878.1|  
|File Copy 256 bufsize 500 maxblocks| 108403.5| KBps| 30.0 s| 2|1655.0| 655.0|  
|File Copy 4096 bufsize 8000 maxblocks| 813482.5| KBps| 30.0 s| 2|5800.0| 1402.6|  
|Pipe Throughput| 656602.5| lps| 10.0 s| 7| 12440.0| 527.8|  
|Pipe-based Context Switching| 26988.5| lps| 10.0 s| 7| 4000.0|67.5|  
|Process Creation| 2558.0| lps| 30.0 s| 2| 126.0| 203.0|  
|Shell Scripts (1 concurrent)| 1233.7| lpm| 60.0 s| 2| 42.4|291.0|  
|Shell Scripts (8 concurrent)| 1119.0| lpm| 60.0 s| 2| 6.0|1865.0|  
|System Call Overhead| 1031068.0| lps| 10.0 s| 7| 15000.0|687.4|  
|System Benchmarks Index Score:| | | | | | 500.7|  

#### 4 parallel processes

|Test| Score| Unit| Time| Iters.| Baseline| Index|  
|:---|---:|:---|---:|---:|---:|---:|
|Dhrystone 2 using register variables| 57870650.9| lps| 10.0 s| 7|116700.0| 4958.9|  
|Double-Precision Whetstone| 10155.4| MWIPS| 9.6 s| 7| 55.0|1846.4|  
|Execl Throughput| 8951.1| lps| 29.9 s| 2| 43.0| 2081.6|  
|File Copy 1024 bufsize 2000 maxblocks| 725711.1| KBps| 30.0 s| 2|3960.0| 1832.6|  
|File Copy 256 bufsize 500 maxblocks| 229203.3| KBps| 30.0 s| 2|1655.0| 1384.9|  
|File Copy 4096 bufsize 8000 maxblocks| 1838586.1| KBps| 30.0 s|2| 5800.0| 3170.0|  
|Pipe Throughput| 2376358.0| lps| 10.0 s| 7| 12440.0| 1910.3|  
|Pipe-based Context Switching| 367444.3| lps| 10.0 s| 7| 4000.0|918.6|  
|Process Creation| 25032.3| lps| 30.0 s| 2| 126.0| 1986.7|  
|Shell Scripts (1 concurrent)| 7570.2| lpm| 60.0 s| 2| 42.4|1785.4|  
|Shell Scripts (8 concurrent)| 1252.9| lpm| 60.1 s| 2| 6.0|2088.1|  
|System Call Overhead| 3797050.7| lps| 10.0 s| 7| 15000.0|2531.4|  
|System Benchmarks Index Score:| | | | | | 2035.0|  
