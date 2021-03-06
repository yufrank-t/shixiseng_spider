# 实习僧网站爬虫
## 爬虫具体内容

Python3.5 编写

实现了几个功能：

- 对隐藏信息类的反爬机制攻克
  - 详细攻克原理和过程写在blog里：[攻破网页字符替换反爬虫机制小记](https://ysbbswork.github.io/2018/03/13/%E6%94%BB%E7%A0%B4%E7%BD%91%E9%A1%B5%E5%AD%97%E7%AC%A6%E6%9B%BF%E6%8D%A2%E5%8F%8D%E7%88%AC%E8%99%AB%E6%9C%BA%E5%88%B6%E5%B0%8F%E8%AE%B0/)
- font文件下载，排重，解析
- MongoDB数据库的读写

## 网页隐藏信息的反爬机制

因为要找实习的缘故，想把实习网站上某个类目下的所有实习职位进行爬取。

选择的网站为 [实习僧](https://www.shixiseng.com/)，但是在爬取的过程中发现了一个网站的反爬机制。

网站将重要的信息通过自定义font文件的方式，进行网页中关键文字的替换，

在实习僧网页爬取中体现为实习金额等关键数据：

![](http://ww1.sinaimg.cn/large/005HFdfGgy1fpb9y3c6byj30vz0mp10p.jpg)

关键的数据圈闭都是显示为乱码的方框状的，无法正确显示和爬取，很显然，是遇到了网站的反爬机制。

这个情况在 猫眼电影，汽车之家论坛都有遇见，是一个非常有效的反爬机制，也是很常见的网页数据隐藏的反爬机制。

## 补充

因为网站的font文件每隔一段时间会变动，第一次启动爬虫需要下载其自定义的加密font并解析，所以第一次启动会比较慢。需要等待文件下载。

之后只要网站font文件不变化就不会下载，每次自动检测网站加密文章的font文件是否改变，如果改变，再重新下载。

根据规律，一般网站的font文件是有限的，多次下载之后，就拿到了几乎网站全部的font文件，每次只需要本地读写，速度会一次比一次快。