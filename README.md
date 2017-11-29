# forSSD_txt2xml

用caffe实现SSD中，从txt文件格式到xml转变


> 该份代码改编自博客：http://www.cnblogs.com/objectDetect/p/5780006.html


代码的功能：
 - 1、将每张照片信息，变为xml格式
 - 2、支持多标签，不再是一个图片一个标签框
 - 3、如果标签中的物体Box有误：Box值多了的话，取前4个值；Box值少了的话，会主动跳过。
 - 4、报错内容的图像ID会输出成list文件：wrong_list

```
object_number
className x1min y1min x1max y1max
classname x2min y2min x2max y2max
```
其中object_number可以是图片名字，不带.jpg，后面的xml解析的时候会根据这个识别图片名称；className 是物体框类别的名称，不是数字哟

具体样例在example之中可以看到，需要前两个文件夹：JPEGImages（存放照片）、label（每张照片一个label）生成第三个文件夹：Annotations

代码中，需要修改的部分已经用#matt标识。

## 如何从csv->txt
csv的格式
```
name	coord
1	[1,2,3,4]
2	[1,2,3,4]
3	[1,2,3,4]
2	[2,3,4,5]
3	[4,5,6,7]
```
然后用以下的方式把内容以txt保存到指定位置：
```
import pandas as pd
data = pd.read_csv('../.csv')

only_id = list(set(data ['name']))
save_annations_path = '../laebl/'

for oid in tqdm(list(only_id)):
    txt_test = copy.copy(oid)
    tmp_data = data[data['name']==oid]
    for i in range(len(tmp_data)):
        xmin,ymin,xmax,ymax = eval(list(tmp_data['coord'])[i])
        txt_test = txt_test + '\n' + 'yz '+ ' '.join([str(xmin),str(ymin),str(xmax),str(ymax)])
    with open(save_annations_path + oid+'.txt',"w") as f:
        f.write(txt_test)
```


Matt/2017-5-4
本人博客:http://blog.csdn.net/sinat_26917383/article/details/68068113
