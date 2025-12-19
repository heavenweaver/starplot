This directory contains the raw data that will be used in translating text in Starplot to chinese languages(zh-TW).
<img width="2005" height="2004" alt="starchart_test_TW" src="https://github.com/user-attachments/assets/7b05e465-f67c-41b4-a07b-bdeedeed2efc" />
## Basic Usage

To create a star chart for tonight's sky in Asia/Taipei:

```python
# -*- coding: utf-8 -*-
'''
import matplotlib as mpl
mpl.rcParams['font.family'] = ['serif']
mpl.rcParams['font.serif'] = ['Noto Sans TC']
'''
from datetime import datetime
from zoneinfo import ZoneInfo

from starplot import ZenithPlot, settings, Observer, _
from starplot.styles import PlotStyle, LabelStyle, LegendStyle, extensions

#from starplot.styles import fonts
#fonts.load()

tz = ZoneInfo("Asia/Taipei")
print("現在時間 : ",datetime.now(tz))
#dt = datetime.now(tz)
# Observering time
dt = datetime.now(tz).replace(day=15,hour=20,minute=00)
dt_format = dt.strftime("%Y/%m/%d %H:%M")  
print("觀測時間 : ",dt_format)
dt_print = dt.strftime("%Y-%m-%d %H:%M") 

observer = Observer(
    dt=dt,
    #lat=33.363484,
    #lon=-116.836394,
    lat=25.04776,
    lon=121.53185,
)

# Local Language Setting 
#settings.language =  "en-us"
#settings.language =  "fr"
settings.language = "zh-TW"

style=PlotStyle().extend(
        extensions.BLUE_GOLD,
        extensions.GRADIENT_PRE_DAWN,
    )

p = ZenithPlot(
    observer=observer,
    style=style,
    resolution=3600,
    autoscale=True,
)
#-------- Style Label Font Name Setting --------------
style.legend = LegendStyle()
style.legend.font_name= 'Noto Sans TC'
style.legend.title_font_name = 'Noto Sans TC'

style.constellation_labels.font_name = 'Noto Sans TC'
style.ecliptic.label.font_name = 'Noto Sans TC'
style.celestial_equator.label.font_name = 'Noto Sans TC'
style.horizon.label.font_name = 'Noto Sans TC'
style.star.label.font_name = 'Noto Sans TC'
style.moon.label.font_name = 'Noto Sans TC'
style.planets.label.font_name= 'Noto Sans TC'
#------------------------------------------------------

p.stars(where=[_.magnitude < 4.6], where_labels=[_.magnitude < 2.1])
p.galaxies(where=[_.magnitude < 6], true_size=False, where_labels=[False])
p.open_clusters(where=[_.magnitude < 6], true_size=False, where_labels=[False])

p.moon()
p.planets()
p.horizon()
p.constellations()
p.constellation_labels()
p.ecliptic()
p.celestial_equator()
p.milky_way()

p.legend("台北市  "+ dt_print)
#p.legend("Asia/Taipei  "+ dt_print)

'''
p.marker(
    ra=12.36 * 15,
    dec=25.85,
    style={
        "marker": {
            "size": 60,
            "symbol": "circle",
            "fill": "none",
            "color": None,
            "edge_color": "hsl(44, 70%, 73%)",
            "edge_width": 2,
            "line_style": [1, [2, 3]],
            "alpha": 1,
            "zorder": 100,
        },
        "label": {
            "zorder": 200,
            "font_size": 22,
            "font_weight": "bold",
            "font_color": "hsl(44, 70%, 64%)",
            "font_alpha": 1,
            "offset_x": "auto",
            "offset_y": "auto",
            "anchor_point": "top right",
        },
    },
    label="Mel 111",
)
'''
p.export("Starchart_TW.png", transparent=True, padding=0.1)
```
## How to Make sky.db and Update zh-TW Translations Manually
Detailed processes step by step.<br/>
At First, please check those csv files are ready.

1.Only zh-TW Translations(iau_id,English,zh-TW)<br/>
	/Users/user/Downloads/starplot/data/raw/translations/zh-tw<br/>
- 	constellation_names.csv, <br/>   	
-	dso_names.csv, <br/>   	
-	other_terms.csv, <br/>   	
-	star_names.csv, 

2.Summarize Translations (iau_id,English,French,Farsi,zh-CN,zh-TW) <br/>
	/Users/user/Downloads/starplot/data/raw/translations<br/>   	
-	constellation_names.csv,<br/>
-  	dso_names.csv, <br/>   	
-	other_terms.csv, <br/>   	
-	star_names.csv

3.RUN python3 data/scripts/db.py<br/>

4.Check sky.db file is exist.<br/>
-  cd /Users/user/Downloads/starplot/data/build<br/>
-  /Users/user/Downloads/starplot/data/build/sky.db

5.Edit translations.py<br/>
-	/Users/user/Downloads/starplot/data/scripts/translations.py, <br/>
-	Add below code into translations.py, after "zh-cn" segment/block.
  
  ---------------------
  ```python
    "zh-tw": {
        "legend": "圖例",
        "star magnitude": "星等",
        "star": "恆星",
        "deep sky object": "深空天體",
        "open cluster": "疏散星團",
        "globular cluster": "球狀星團",
        "nebula": "星雲",
        "galaxy": "星系",
        "dark nebula": "暗星雲",
        "association of stars": "星協",
        "double star": "雙星",
        "emission nebula": "發射星雲",
        "galaxy pair": "星系對",
        "galaxy triplet": "三重星系",
        "galaxy cluster": "星系團",
        "group of galaxies": "星系群",
        "hii ionized region": "hii電離氫區",
        "nova star": "新星",
        "planetary nebula": "行星狀星雲",
        "reflection nebula": "反射星雲",
        "star cluster nebula": "星團星雲",
        "supernova remnant": "超新星遺蹟",
        "unknown": "未知天體",
        "planet": "行星",
        "mercury": "水星",
        "venus": "金星",
        "mars": "火星",
        "jupiter": "木星",
        "saturn": "土星",
        "uranus": "天王星",
        "neptune": "海王星",
        "pluto": "冥王星",
        "sun": "太陽",
        "moon": "月球",
        "north": "北",
        "east": "東",
        "south": "南",
        "west": "西",
        "ecliptic": "黃道",
        "celestial equator": "天赤道",
        "n": "北",
        "e": "東",
        "s": "南",
        "w": "西",
        "milky way": "銀河",
    },
```
  ---------------

6.Copy sky.db and translations.py to the starplot installed directory to replace old version.<br/>
 e.g. /Users/user/miniconda3/lib/python3.13/site-packages/starplot<br/>
- ./data/translations.py
- ./data/library/sky.db
## Traditional Chinese astronomy: the Twenty-Eight Mansions (Chinese: 二十八宿)
<img width="995" height="992" alt="NorthPoleEquidistant_01" src="https://github.com/user-attachments/assets/29d9b826-9eee-46a0-bfb4-c362b5432bbc" />
