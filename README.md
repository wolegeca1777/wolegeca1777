- š Hi, Iām @wolegeca1777
- š Iām interested in ...
- š± Iām currently learning ...
- šļø Iām looking to collaborate on ...
- š« How to reach me ...

<!---
wolegeca1777/wolegeca1777 is a āØ special āØ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
---
import os
import xlrd
from tqdm import tqdm
import seaborn as sns
from pandas import Series,DataFrame
import pandas as pd
import numpy as np
import csv
import matplotlib.pyplot as plt
import xlwings as xw
import shutil
import time
from docx import Document
from docx.shared import Inches
from decimal import Decimal
import locale
from datetime import datetime
from dateutil.relativedelta import relativedelta
import chardet
import random
import collections
import re
import requests
import winsound
import json
import time
from requests_toolbelt import MultipartEncoder


%%time
td = time.strftime("%Y-%m-%d")
df = pd.DataFrame()


def go_list(n = 1):

    html = requests.get(
                        url='https://car.xiaojuchefu.com/api-gateway/carApi/inStorage/list',
        
                        headers={
                                    "Cookie": '_ga=GA1.2.1993957949.1618707965; _gid=GA1.2.332455144.1622893689; Hm_lvt_21ec203bf0297b63e6a55433a8c9b067=1622465155,1622637540,1622893689,1622953481; NewSSO_SESSIONID=N2NSOSt1clZaUFIxQVRKcFBaQ2IxSGxoczJPSzBzWGlTaktEdlEyTFNaRGV0RnpiNG9BeWlNRUZsVFhYM3hjNA%3D%3D; SSO_SESSIONID=N2NSOSt1clZaUFIxQVRKcFBaQ2IxSGxoczJPSzBzWGlTaktEdlEyTFNaRGV0RnpiNG9BeWlNRUZsVFhYM3hjNA%3D%3D; NewAutoCompanyUser=bDA5bkhxUk9MR29tTmg4SGFVcFZwRnVMcjhEOGVMWGVER3VoWHA0cHlwWTFqWjNOUWZKNEZHR2dPSTJSM1ZieGFra2tua0kwSGRoQXlSVWE1RGxjOUg5OU5JNVlUclo4cm9seDRKS1FXTEdiZGRyWUtDTG9ucjZXRkVlN25td3pMbDBYcTlzd2VnSEZNK1hMdko3di9sZ1doa0ZkYnJqazV5OEw5K2VpcXN0TTF6MnBLU0lvNnR0TXhrTy8wV0lK; AutoCompanyUser=bDA5bkhxUk9MR29tTmg4SGFVcFZwRnVMcjhEOGVMWGVER3VoWHA0cHlwWTFqWjNOUWZKNEZHR2dPSTJSM1ZieGFra2tua0kwSGRoQXlSVWE1RGxjOUg5OU5JNVlUclo4cm9seDRKS1FXTEdiZGRyWUtDTG9ucjZXRkVlN25td3pMbDBYcTlzd2VnSEZNK1hMdko3di9sZ1doa0ZkYnJqazV5OEw5K2VpcXN0TTF6MnBLU0lvNnR0TXhrTy8wV0lK; Hm_lpvt_21ec203bf0297b63e6a55433a8c9b067=1622953512; __hash__wa=20210606-car-232031-f7a685bd-8ac9-448b-85d7-7a0612d73e12; __hash__cache=f7a685bd-8ac9-448b-85d7-7a0612d73e12; user-fingerprint-water-mark=20210606-car-232031-f7a685bd-8ac9-448b-85d7-7a0612d73e12',
                                    #"Host": "car.xiaojuchefu.com",

                                    'referer': 'https://car.xiaojuchefu.com/car-management/sheets-income/list',

                                    "User-Agent": 'Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/78.0.3904.108 Safari/537.36',
                                    "X-Auto-Company-ID": "37782",
                                    "X-Requested-With": "XMLHttpRequest",
                                },
        
                        params = {
                                    'size': 10,
                                    'page': n,
                                    #'finishedTime': '2021-05-01 05:40:46,2021-06-30 23:40:46'
                                    
                                }


                                                    )

    return html.json()

page = go_list()["data"]["pagination"]["total_pages"]

print(f"å±č®”{page}é”µę°ę®")


for i in range(1,page+1):
    go_data = pd.DataFrame(go_list(n=i)["data"]["list"])
    df = df.append(go_data)
    print(f"{i}é”µå·²å®ę")
    
    
    
df.rename(columns={"appointTimeStart":"é¢ēŗ¦å„åŗę¶é“",
                   "cityName":"ååø",
                   "cpName":"å¬åø",
                   "createTime":"åå»ŗę¶é“",
                   "deliveryCenterName":"äø­åæä»",
                   "finishedTime":"ē»ęę¶é“",
                   "id":"å·„åē¼å·",
                   "plateNo":"č½¦ēå·",
                   "statusStr":"å·„åē¶ę",
    
                    },
          inplace = True
         )

df = df[['č½¦ēå·','é¢ēŗ¦å„åŗę¶é“','ååø','å¬åø','åå»ŗę¶é“','äø­åæä»','ē»ęę¶é“','å·„åē¶ę','å·„åē¼å·']]
df.reset_index(inplace=True,drop=True)
df.to_excel(f"C:\\Users\\sun'jun\\Desktop\\ęÆę„ę“ę°\\test/å„åŗå·„åäæ”ęÆ.xlsx")
xw.Book(f"C:\\Users\\sun'jun\\Desktop\\ęÆę„ę“ę°\\test/å„åŗå·„åäæ”ęÆ.xlsx")
