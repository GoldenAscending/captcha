## Captcha with background images

## Usage

![](http://transing.bj.bcebos.com/image/11.png)
```

`
#coding:utf-8
from captcha.image import ImageCaptcha  # pip install captcha
import cv2
import numpy as np
from matplotlib import pyplot as plt
import random,time
from PIL import Image

number = ['0','1','2','3','4','5','6','7','8','9']
alphabet = ['a','b','c','d','e','f','g','h','i','j','k','l','m','n','o','p','q','r','s','t','u','v','w','x','y','z']
ALPHABET = ['A','B','C','D','E','F','G','H','I','J','K','L','M','N','O','P','Q','R','S','T','U','V','W','X','Y','Z']

def random_captcha_text(char_set=number+alphabet+ALPHABET, captcha_size=4):
    captcha_text = []
    for i in range(4):
        c = random.choice(char_set)
        captcha_text.append(c)
    return captcha_text

def gen_captcha():
    image = ImageCaptcha()
    #extract image edges
    bf = cv2.imread('five.png',0)
    bf = cv2.resize(bf, (32, 32))
    bf = cv2.Canny(bf,100,200)
    bf = cv2.bitwise_not(bf)
    
    captcha_text = random_captcha_text()
    ex = Image.fromarray(bf)
    captcha = image.generate(captcha_text, images=[ex, ex])
    img = Image.open(captcha)
    img = np.array(img)
    return img

plt.imshow(gen_captcha())
plt.show()
`
