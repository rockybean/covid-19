Name
====
Covid-19 @ Kibana

Let's analyze covid-19 outbreak in Elastic Stack!


Table of Contents
=================
- [Name](#name)
- [Table of Contents](#table-of-contents)
- [Dashboard](#dashboard)
- [Architecture](#architecture)
- [Requirements](#requirements)
- [Usage](#usage)
- [Author](#author)


Dashboard
======
Final Kibana Dashboard is as below:
![](https://cdn.nlark.com/yuque/0/2020/png/113753/1583931944219-f5031ece-3d6e-4e16-bb86-252affd35dd6.png)


Architecture
=======
![](https://cdn.nlark.com/yuque/0/2020/png/113753/1583713594293-0f3be6b9-0a48-4bef-9632-73e5cc4108bd.png)

1. I finally choose to write a python script to  crawl, filter, transform data from an api service into es. Because it's too hard to split one api response to many events in logstash.
2. I setup es and kibana instance on top of elastic cloud service. It's super easy and awesome. Sass is wonderful.
3. I build this demo dashboard on top of kibana.


Requirements
============
* Python 3
* pip install requests,elasticsearch

Usage
=====

> This script can only download latest data now because the api server has stopped to support 'latest=0' parameter.
>https://lab.isaaclin.cn/nCoV/en

1. Import covid-19 data
* Download covid-19.py
* Run following command
  ```
  ES_URL=http://127.0.0.1:9200 ES_USERNAME=elastic ES_PASSWD=passwd python covid-19.py
  ```
  * ES_URL is your es service endpoint
  * ES_USERNAME is your es username and ignore this if you don't enable security feature
  * ES_PASSWD is your es password and ignore this if you don't enable security feature
* **covid-19.py** will do following work.
  * Check if there is **covid-19-data** index in your es instance.
  * If no, it will create **covid-19-data** index with custom settings and mapping. Then it will download all historical covid-19 data and export to your es in **covid-19-data** index.
  * If yes, it will only download latest covid-19 data.
  * It will keep only one record per day for each country,province or city which will make our analysis job easier.

2. Import kibana objects
* Download covid-19-kibana-7.6.1.ndjson
* Import this in following kibana page.
![](https://cdn.nlark.com/yuque/0/2020/png/113753/1583712551434-bbac3b8c-8cc7-43f5-82b5-b1269df8b2a4.png?x-oss-process=image/resize,w_1492)

3. Start to play your own covid-19 data!

Feel free to open an issue or pull request!

Author
======
* Rockybean
    * [github](https://github.com/rockybean)
    * [twitter](https://twitter.com/imrockybean)