# forSSD_txt2xml

用caffe实现SSD中，从txt文件格式到xml转变


> 该份代码改编自博客：http://www.cnblogs.com/objectDetect/p/5780006.html


代码的功能：
 - 1、将每张照片信息，变为xml格式
 - 2、支持多标签，不再是一个图片一个标签框
 - 3、如果标签中的物体Box有误：Box值多了的话，取前4个值；Box值少了的话，会主动跳过。
 - 4、报错内容的图像ID会输出成list文件：wrong_list


样例在example之中可以看到，需要两个文件夹：JPEGImages（存放照片）、label（每张照片一个label）生成第三个文件夹：Annotations

Matt/2017-5-4
