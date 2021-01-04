# Aidea
## AI CUP 2020  和弦辨識競賽  
* 資料來自[和弦辨識競賽](https://aidea-web.tw/topic/43d9cc47-b70e-4751-80d3-a2d7333eb77b)

## 資料預處理 

``` python
from glob import glob
from shutil import copyfile
import os
os.mkdir('Aidea/data/ce200')
os.mkdir('Aidea/data/ce200/annotations')
os.mkdir('Aidea/data/ce200/annotations/Labels')
os.mkdir('Aidea/data/ce200/audio')
f = open('Aidea/data/ce200/annotations/Labels.txt','a')
for i in range(1,201):
    try:
        
        #copy label file and delete last line
        src_label = 'CE200/{}/ground_truth.txt'.format(i)
        dst_label = 'Aidea/data/ce200/annotations/Labels/{0:03d}.txt'.format(i)
        with open(src_label) as f1:
            lines = f1.readlines()
            
        with open(dst_label, 'w') as f2:
            f2.writelines(lines[:-1])
        
        #copy mp3 file
        src_mp3 = glob('CE200/{}/*.mp3'.format(i))
        dst_mp3 = 'Aidea/data/ce200/audio/{0:03d}.mp3'.format(i)
        copyfile(src_mp3[0], dst_mp3)
        
        f.write('Labels/{0:03d}.txt\n'.format(i))
    except:
        print('copy fail in',i)

f.close()
```

```bash
├── data
│   ├── assets
│   │   ├── model
│   │   ├── result
│   │   └── tensorboard
│   ├── ce200
│   │   ├── annotations
│   │   └── audio
│   └── result
```
