# TF-serving 部署自己的模型

**第一步：** 安装必须的环境，conda/tensorflow/cudnn/docker等，教程非常多

**第二步：** 运行demo
```python
docker pull tensorflow/serving
git clone https://github.com/tensorflow/serving
docker run -t --rm -p 8501:8501 \
    -v "D:/codes/docker-codes/docker-tfserving/serving/tensorflow_serving/servables/tensorflow/testdata/saved_model_half_plus_two_cpu:/models/half_plus_two" \
    -e MODEL_NAME=half_plus_two \
    tensorflow/serving '&'
```

模型预测：

![图片](https://github.com/onlyone2019/notes/blob/master/pictures/TF-serving_demo.png)

[参考](https://tensorflow.google.cn/tfx/serving/docker?hl=zh-cn)


**第三步：** 部署自己的模型
- 1.将自己的模型保存，生成variables文件夹和saved_model.pb
- 2.找到第二步中 D:/codes/docker-codes/docker-tfserving/serving/tensorflow_serving/servables/tensorflow/testdata 这个路径，在testdata下新建一个文件夹 cloth_classify，然后在cloth_classify里创建一个版本文件夹000001，并将variables文件夹和saved_model.pb放入其中
- 3.部署模型：`docker run -p 8999:8501 --mount type=bind,source=D:/codes/docker-codes/docker-tfserving/serving/tensorflow_serving/servables/tensorflow/testdata/cloth_classify,target=/models/cloth_classify -e MODEL_NAME=cloth_classify -t tensorflow/serving '&'`

查看模型是否部署成功：

![图片](https://github.com/onlyone2019/notes/blob/master/pictures/TF-serving_firstModel.png)