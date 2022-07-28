import numpy as np
import cv2

def calc():
    path= r"21.png"  # 选择图片
    img=cv2.imdecode(np.fromfile(path,dtype=np.uint8),-1) # cv2.imread只能读取英文路径下的图片，若要读取中文路经下的图片需要用cv2.imdecode，否则读取到的图片内容为none，cv2.imdecode也可以用来读取英文路径下的图片
    # cv2.imshow("The original image",img)

    img_gray=cv2.cvtColor(img,cv2.COLOR_BGR2GRAY) # 表示从BGR转换位灰度图像。
    # cv2.imshow("Gray image",img_gray)

    # cv2.waitKey()
    # cv2.destroyAllWindows()

    rows,cols=img_gray.shape
    img_gray=np.uint16(img_gray)
    n=np.zeros((256,256))
    # img_gray[i,j]是像素的灰度值，k是区域灰度
    IJ=[] # 记录点灰度与区域灰度的对应值
    for i in range(rows):
        for j in range(cols):
            if i==0:
                if j==0:
                    k=(img_gray[i][j]+img_gray[i][j+1]+img_gray[i+1][j]+img_gray[i+1][j+1])/4
                elif j==cols-1:
                    k=(img_gray[i][j-1]+img_gray[i][j]+img_gray[i+1][j-1]+img_gray[i+1][j])/4
                else:
                    k=(img_gray[i][j-1]+img_gray[i][j]+img_gray[i][j+1]+img_gray[i+1][j-1]+img_gray[i+1][j]+img_gray[i+1][j+1])/6
            elif i==rows-1:
                if j == 0:
                    k=(img_gray[i-1][j]+img_gray[i-1][j+1]+img_gray[i][j]+img_gray[i][j+1])/4
                elif j==cols-1:
                    k=(img_gray[i-1][j-1]+img_gray[i-1][j]+img_gray[i][j-1]+img_gray[i][j])/4
                else:
                    k=(img_gray[i-1][j-1]+img_gray[i-1][j]+img_gray[i-1][j+1]+img_gray[i][j-1]+img_gray[i][j]+img_gray[i][j+1])/6
            elif j==0:
                if i!=0 and i!=rows-1:
                    k=(img_gray[i-1][j]+img_gray[i-1][j+1]+img_gray[i][j]+img_gray[i][j+1]+img_gray[i+1][j]+img_gray[i+1][j+1])/6
            elif j==cols-1:
                if i!=0 and i!=rows-1:
                    k=(img_gray[i-1][j-1]+img_gray[i-1][j]+img_gray[i][j-1]+img_gray[i][j]+img_gray[i+1][j-1]+img_gray[i+1][j])/6
            else:
                k=(img_gray[i-1][j-1]+img_gray[i-1][j]+img_gray[i-1][i+1]+img_gray[i][j-1]+img_gray[i][j]\
                   +img_gray[i][j+1]+img_gray[i+1][j-1]+img_gray[i+1][j]+img_gray[i+1][j+1])/9
            # temp=(img_gray[i][j],int(k))
            # IJ.append(temp)
            IJ.append([img_gray[i][j],int(k)])
    print(IJ)
    # 计算n_ij,nij就是这一对灰度-区域灰度在这个图像中出现的次数
    
    n_ij = []
    # 计算n_ij
    arr = [list(i) for i in set(tuple(j) for j in IJ)]
    for i in range(len(arr)):
        n_ij.append(IJ.count(arr[i]))

    # 计算p_ij
    p_ij = np.array(n_ij) / (img_gray.shape[0] * img_gray.shape[1])

    # 计算2d离散熵
    H = 0
    for p in p_ij:
        H += np.sum(p * np.log(1/p))
        
    # 计算2d最大熵
    PA=0
    for i in p_ij:
        PA+=np.sum(i)

    HA=np.log(PA)+(H/PA)
    print(HA)

calc()













