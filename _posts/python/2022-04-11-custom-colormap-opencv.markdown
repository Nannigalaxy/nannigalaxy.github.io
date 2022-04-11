---
layout: post
title:  " OpenCV Custom Colormap"
description:  "Adding custom colormap for opencv"
date:   2022-04-11
last_modified_at: 2022-05-11
categories: Python OpenCV
---
![](/assets/posts/{{page.url}}/header.png)


[Colormap](https://docs.opencv.org/4.x/d3/d50/group__imgproc__colormap.html#ga9a805d8262bcbe273f16be9ea2055a65){:target="_blank"} provided by OpenCV is limited and might suffice for most users but there will senarios where custom colormap is crucial for intended visual representation.  

Now we will see how can create our own colormap using ['Lookup Table'](https://docs.opencv.org/4.x/d2/de8/group__core__array.html#gab55b8d062b7f5587720ede032d34156f){:target="_blank"}.  

### Creating LUT

Let's create a function to handle RGB mappping from the dictionary to image.

```Python  
def cvlut(colordict):
    cmap = collections.OrderedDict()
    cmap = colordict
    crange = 0
    clist = list(cmap.items())
    r = []
    g = []
    b = []
    while(crange < 256):
        for i in range(len(clist)):
            if i != (len(clist) - 1):
                for n in range(clist[i][0], clist[i + 1][0]):
                    r.append(clist[i][1][0])
                    g.append(clist[i][1][1])
                    b.append(clist[i][1][2])
                    crange += 1
            else:
                for n in range(clist[i][0], 256):
                    r.append(clist[i][1][0])
                    g.append(clist[i][1][1])
                    b.append(clist[i][1][2])
                    crange += 1

    lut = np.zeros((256, 1, 3), dtype=np.uint8)
    lut[:, 0, 0] = r
    lut[:, 0, 1] = g
    lut[:, 0, 2] = b

    return lut
```

The above function creates LUT for specified grayscale range.

Now let's see how we can use the created function to apply colormap

```Python
colormap_dict = {0: [0, 0, 0], # grayscale: [R, G, B]
                111: [220, 8, 8], 
                128: [237, 252, 2], 
                171: [8, 220, 85], 
                213: [0, 163, 32]}
custom_lut = cvlut(colormap_dict)
ndvi_color = cv2.LUT(input_gray_image, custom_lut)
```

The color applied is 'Pseudocolor' aka 'False Color' as it is mapping to grayscale image. So, the actual range is between `0-255`, upon which RGB is assigned and produce color image.
In `colormap_dict` dictionary each key specifies range of grayscale to map RGB value till succesive key value. This is rudamentary implementation to test the function. I would suggest to generate colormap file with RGB and load.  

<b> Colormap file example:</b>
```custom_colormap.txt
0	255	255	255
1	250	250	250
2	246	246	246
3	242	242	242
4	238	238	238
5	233	233	233
...
20	170	170	170
21	166	166	166
22	161	161	161
23	157	157	157
24	153	153	153
...
116	155	155	155
117	151	151	151
118	146	146	146
119	141	141	141
120	136	136	136
...
237	255	15	0
238	255	10	0
239	255	5	0
240	255	0	0
241	255	0	15
242	255	0	31
243	255	0	47
...
251	255	0	175
252	255	0	191
253	255	0	207
254	255	0	223
255	255	0	239

```

### Full code

```Python
import cv2
import collections

def cvlut(colordict):
    cmap = collections.OrderedDict()
    cmap = colordict
    crange = 0
    clist = list(cmap.items())
    r = []
    g = []
    b = []
    while(crange < 256):
        for i in range(len(clist)):
            if i != (len(clist) - 1):
                for n in range(clist[i][0], clist[i + 1][0]):
                    r.append(clist[i][1][0])
                    g.append(clist[i][1][1])
                    b.append(clist[i][1][2])
                    crange += 1
            else:
                for n in range(clist[i][0], 256):
                    r.append(clist[i][1][0])
                    g.append(clist[i][1][1])
                    b.append(clist[i][1][2])
                    crange += 1

    lut = np.zeros((256, 1, 3), dtype=np.uint8)
    lut[:, 0, 0] = r
    lut[:, 0, 1] = g
    lut[:, 0, 2] = b

    return lut

if __name__=="__main__":
    image = cv2.imread("path_to_image")

    # Convert Grascale to BGR to have proper dimension for mapping further 
    gray2bgr_img = cv2.cvtColor(image, cv2.COLOR_GRAY2BGR)

    colormap_dict = {0: [0, 0, 0], # grayscale: [R, G, B]
                    111: [220, 8, 8], 
                    128: [237, 252, 2], 
                    171: [8, 220, 85], 
                    213: [0, 163, 32]}

    custom_lut = cvlut(colormap_dict)
    colormap_img = cv2.LUT(gray2bgr_img, custom_lut)

    cv2.imwrite('custom-color_1.jpg', colormap_img)
```