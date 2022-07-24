# 编译环境


下载好本项目代码，cd 到该文件夹下 运行  
  pip install -v -e .

# 修改数据集格式
具体可参考一下代码
  + 修改图像文件 jpg转pgn


````# 显示需要加 # ，Markdown中不需要加
  import os
  import PIL.Image as Image

  def changeJpgToPng(srcPath,dstPath):
    
      image = Image.open(srcPath)
      png_name = str(dstPath)[0:-len('.jpg')] + '.png'
      #image.save(png_name)
      #print(png_name)

      #image = image.convert('RGBA')
      image = image.convert('RGB')
      image.save(png_name)
      

  path = "D:\\boat\\mmrotate\\data\\val\\images"
  f=[]
  for root, dirs, files in os.walk(path):

      f=files
  for file in f:
      filepath=path+'\\'+file
      changeJpgToPng(filepath,path+'1'+'\\'+file)

````

 + 修改注释文件
````
import os

path = "D:\\boat\\mmrotate\\data\\train\\annfiles"
f=[]
for root, dirs, files in os.walk(path):
    print("root:", root)
    print("dirs:", dirs)
    print("files", files)
    f=files
for file in f:
    filepath=path+'\\'+file
    
    with open(filepath,"r") as rd:
        lines=rd.readlines()
        try:
            lines=lines[1:]#去第一行
            for i in range(len(lines)):# 加参数
                l=lines[i]
                l=l.split('\n')[0]
                l+=' 1\n'
                lines[i]=l
            rd= open(filepath,"w")
            rd.writelines(lines)
            f.close()
        except:
            pass
````

然后将其分别放入data/train下对应文件夹

# 训练与测试

训练运行 python tool/train.py

测试 python tool/test.py