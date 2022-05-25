# 郑州中原区天气预报
import requests
import parsel
import pprint
import time
import os
from pynput import mouse, keyboard

m_mouse =mouse.Controller()  # 创建一个鼠标
m_keyboard = keyboard.Controller() # 创建一个键盘
m_mouse.click(mouse.Button.left) # 点击鼠标左键
c = time.localtime().tm_hour#获取当前时
e = time.localtime().tm_min#获取当前分
f = 6
def en(k):
    k.press(keyboard.Key.enter)  # 按下enter
    k.release(keyboard.Key.enter)  # 松开
def on(k):
    k.press(keyboard.Key.ctrl)  # 按下ctrl
    k.press(keyboard.Key.enter)  # 按下enter
    k.release(keyboard.Key.enter)  # 松开
    k.release(keyboard.Key.ctrl)  # 松开
f1 = 24
# 晚上24点说晚安
print(str((f1-c)*60*60-e*60)+'秒后说晚安')
time.sleep((f1-c)*60*60-e*60) # 延迟时间
#time.sleep(5)
m_keyboard.type('阳阳宝贝不早了该睡觉了晚安mua~')
en(m_keyboard)
# 6点 发送天气预报

if c > f:
    f = f+24

print((f-c)*60*60-e*60)
print('需等待大约'+str(f-c)+'小时')


time.sleep((f-c)*60*60-e*60)
# 第一步先把天气预报信息获取
url = 'https://www.tianqi.com/xingyang/'# 输入需要爬取的网站
header = {
    'accept': 'text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9',
    'accept-encoding': 'gzip, deflate, br',
    'accept-language': 'zh-CN,zh;q=0.9,en;q=0.8,en-GB;q=0.7,en-US;q=0.6',
    'cache-control': 'no-cache',
    'cookie': 'cityPy=luoyang; cityPy_expire=1649516241; UM_distinctid=17feac7e656138-005f4b4bc3a3e5-56171958-144000-17feac7e65732; CNZZDATA1275796416=1346292883-1648909644-https%253A%252F%252Fwww.baidu.com%252F%7C1648909644; BAIDU_SSP_lcr=https://www.baidu.com/link?url=Lx-DjUEib6GATrvZUBkbFssBoF0HQ2Tc2Lbc646lOUq&wd=&eqid=80a6aad0000a2bea0000000262486440; Hm_lvt_ab6a683aa97a52202eab5b3a9042a8d2=1648911447; CNZZDATA1277722738=420392124-1648908045-https%253A%252F%252Fwww.tianqi.com%252F%7C1648908045; Hm_lpvt_ab6a683aa97a52202eab5b3a9042a8d2=1648911690',
    'pragma': 'no-cache',
    'referer': 'https://www.tianqi.com/',
    'sec-ch-ua': '" Not A;Brand";v="99", "Chromium";v="99", "Microsoft Edge";v="99"',
    'sec-ch-ua-mobile': '?0',
    'sec-ch-ua-platform': '"Windows"',
    'sec-fetch-dest': 'document',
    'sec-fetch-mode': 'navigate',
    'sec-fetch-site': 'same-origin',
    'sec-fetch-user': '?1',
    'upgrade-insecure-requests': '1',
    'user-agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.74 Safari/537.36 Edg/99.0.1150.55',
}# 获取响应头
three = requests.get(url=url,headers=header)
three.encoding = 'utf-8'# 输入需要爬取的网站
threes = parsel.Selector(three.text)# 获取网页代码
name=threes.css('body > div.weatherbox > div > div.left > dl > dd.weather > span > b::text').get()# 获取文本信息
names=threes.css('body > div.weatherbox > '
                 'div > div.left > dl > dd.weather > span::text').get()
two=threes.css('body > div.weatherbox > div > div.left > dl > dd.name > h1::text').get()
twos=threes.css('body > div.weatherbox > div > div.left > dl > dd.kongqi > h5::text').get()
one=threes.css('body > div.weatherbox > div > div.left > dl > dd.kongqi > span').get()
fours=threes.css('body > div.weatherbox > div > div.left > dl > dd.kongqi > span::text').get()
four = one[19]+one[20]+one[21]+one[22]+one[23]+one[24]+one[25]+one[26]+one[27]#截取有用的文本
five = threes.css('body > div.weatherbox > div > div.left > dl > dd.week::text').get()
# 第二步创建自动编辑短信
print(time.localtime().tm_min)
b = str(time.localtime().tm_year)+'年'+str(time.localtime().tm_mon)+'月天气预报'
if not os.path.exists(b):
    # 创建文件夹
    os.makedirs(b)
with open(b + '\\' +str(time.localtime().tm_mday)+'号.txt',mode="a", encoding="utf-8") as f:
    f.write(five)
    f.write('\n')
    f.write(two)
    f.write('\n')
    f.write(name)
    f.write('\n')
    f.write(names)
    f.write('\n')
    f.write(twos)
    f.write('\n')
    f.write(fours)
    f.write('\n')
    f.write(four)
    f.write('\n')
m_keyboard.type('阳阳宝贝这是今天的天气预报')
en(m_keyboard)
m_keyboard.type(five)
on(m_keyboard)
m_keyboard.type(two)
on(m_keyboard)
m_keyboard.type(name)
on(m_keyboard)
m_keyboard.type(names)
on(m_keyboard)
m_keyboard.type(twos)
on(m_keyboard)
m_keyboard.type(fours)
on(m_keyboard)
m_keyboard.type(four)
en(m_keyboard)
z = time.localtime().tm_hour#获取当前时
# 8点 提醒吃饭
f2 = 2*60*60
print(f2)
print('需等待大约'+str(f2)+'秒')
time.sleep(f2)
m_keyboard.type('阳阳宝贝早安')
en(m_keyboard)
m_keyboard.type('起床了该吃早饭了')
en(m_keyboard)
