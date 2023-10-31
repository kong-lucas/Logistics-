# Logistics-
Logistic 
import requests
from dateutil import parser #解析器
from datetime import datetime, time
from time import sleep
def get_tick(stock_code):
    if stock_code[0] == "6":
        prefix = "sh"
    elif stock_code == "0":
        prefix = "sz"
    else:
        raise Exception("参数错误")
    page = requests.get("http://qt.gtimg.cn/q="+prefix+stock_code)
    stock_info = page.text
    stock_info = stock_info.split("~")
    op = float(stock_info[5])
    high = float(stock_info[33])
    low = float(stock_info[34])
    close = float(stock_info[3])
    trade_datatime = parser.parser(stock_info[30])
    return [trade_datatime,close]
if __name__  == "__main__":
    stock_c = "600036"
    dt,close = get_tick(stock_c)
    print(stock_c,dt,close)

def stratege(tick):
