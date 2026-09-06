# tdxquant
tdx quant

TdxQuant 以 tqcenter 行情模块为核心，主要包含以下内容：

行情数据：实时与历史的快照、K 线、分笔（Tick）数据

基本面数据：除权除息、基本财务、专业财务、股票交易数据、市场数据等

新股和合约等信息：标的基础信息、可转债、新股申购等

分类数据：市场类型、行业分类、自定义板块等

## 行情数据

实时与历史的快照、K 线、分笔（Tick）数据

### 刷新行情缓存 - tq.refresh_cache()

~~~
'''
    刷新行情缓存 刷新后5分钟内取最新report和k线数据不会触发刷新
    force参数表示是否强制刷新 默认False
    market参数表示指定市场刷新
    'AG'表示A股 'HK'表示港股 'US'表示美股 'QH'表示期货  'QQ'表示期权  'ZZ'表示中证国证指数 'ZS' 表示沪深京指数
'''
refresh_cache = tq.refresh_cache()
print(refresh_cache)

~~~

output

~~~
TQ数据接口初始化成功，使用路径: d:\Thirdprogram\newtdxtqv772\PYPlugins\user\tdxdata_test_demo.py
{"ErrorId":"0","Msg":"Refresh Cache Success.","run_id":"2"}
~~~

## 基本面数据

除权除息、基本财务、专业财务、股票交易数据、市场数据

###  获取分红送配数据 - tq.get_divid_factors

~~~
divid_factors = tq.get_divid_factors(
        stock_code='688318.SH',
        start_time='',
        end_time='')
print(divid_factors)
~~~

output

~~~
           Type  Bonus  AllotPrice  ShareBonus  Allotment
Date                                                     
2020-09-29    1    6.0         0.0         0.0        0.0
2021-05-27    1   10.0         0.0         0.0        0.0
2022-06-20    1   14.0         0.0         4.0        0.0
2023-06-13    1    5.0         0.0         4.0        0.0
2024-06-14    1    8.0         0.0         4.0        0.0
2024-10-18    1    1.1         0.0         0.0        0.0
2025-06-06    1    5.0         0.0         4.0        0.0
2026-06-05    1    3.8         0.0         4.0        0.0

~~~

###  获取市场快照数据 - tq.get_market_snapshot

~~~
'''
    获取市场快照数据,调用会触发客户端刷新数据，耗时过长请耐心等待
    总成交额为万位，其他无特殊说明均为个位
    曾用名：get_full_tick get_report_data
'''
tq.refresh_cache(force=True)
market_snapshot = tq.get_market_snapshot(stock_code = '300078.SZ', field_list=[])
print(market_snapshot)

print(json.dumps(market_snapshot, indent=4, ensure_ascii=False))

~~~

output

~~~
{
    "ErrorId": "0",
    "ItemNum": "2332",
    "LastClose": "2.87",
    "Open": "2.84",
    "Max": "2.96",
    "Min": "2.82",
    "Now": "2.83",
    "Volume": "289706",
    "NowVol": "1318",
    "Amount": "8362.57",
    "Inside": "160425",
    "Outside": "129281",
    "TickDiff": "0.00",
    "InOutFlag": "2",
    "Jjjz": "0.00",
    "Buyp": [
        "2.83",
        "0.00",
        "0.00",
        "0.00",
        "0.00"
    ],
    "Buyv": [
        "1633",
        "0",
        "0",
        "0",
        "0"
    ],
    "Sellp": [
        "2.85",
        "0.00",
        "0.00",
        "0.00",
        "0.00"
    ],
    "Sellv": [
        "1411",
        "0",
        "0",
        "0",
        "0"
    ],
    "UpHome": "0",
    "DownHome": "0",
    "Before5MinNow": "2.82",
    "Average": "2.89",
    "XsFlag": "2",
    "Zangsu": "0.35",
    "ZAFPre3": "2.54"
}

~~~

## 分类数据

市场类型、行业分类、自定义板块等

### 获取A股全部板块 - tq.get_sector_list

~~~
print('获取A股全部板块')
block_list = tq.get_sector_list(list_type=1)
print(block_list)
print(len(block_list))

~~~

output

~~~
[
  {
    "Code": "880081.SH",
    "Name": "轮动趋势"
  },
  {
    "Code": "880082.SH",
    "Name": "板块趋势"
  },
  {
    "Code": "880201.SH",
    "Name": "黑龙江"
  },
  {
    "Code": "880202.SH",
    "Name": "新疆板块"
  },
  {
    "Code": "880203.SH",
    "Name": "吉林板块"
  },
  {
    "Code": "880204.SH",
    "Name": "甘肃板块"
  },
  {
    "Code": "880205.SH",
    "Name": "辽宁板块"
  },
  {
    "Code": "880206.SH",
    "Name": "青海板块"
  },
  {
    "Code": "880207.SH",
    "Name": "北京板块"
  },
  {
    "Code": "880208.SH",
    "Name": "陕西板块"
  },
  {
    "Code": "880209.SH",
    "Name": "天津板块"
  },
  {
    "Code": "880210.SH",
    "Name": "广西板块"
  },
  {
    "Code": "880211.SH",
    "Name": "河北板块"
  },
  {
    "Code": "880212.SH",
    "Name": "广东板块"
  },
  {
    "Code": "880213.SH",
    "Name": "河南板块"
  },
  {
    "Code": "880214.SH",
    "Name": "宁夏板块"
  },
  {
    "Code": "880215.SH",
    "Name": "山东板块"
  },
  {
    "Code": "880216.SH",
    "Name": "上海板块"
  },
  {
    "Code": "880217.SH",
    "Name": "山西板块"
  },
  {
    "Code": "880218.SH",
    "Name": "深圳板块"
  },
  {
    "Code": "880219.SH",
    "Name": "湖北板块"
  },
  {
    "Code": "880220.SH",
    "Name": "福建板块"
  },
  {
    "Code": "880221.SH",
    "Name": "湖南板块"
  },
  {
    "Code": "880222.SH",
    "Name": "江西板块"
  },
  {
    "Code": "880223.SH",
    "Name": "四川板块"
  },
  {
    "Code": "880224.SH",
    "Name": "安徽板块"
  },
  {
    "Code": "880225.SH",
    "Name": "重庆板块"
  },
  {
    "Code": "880226.SH",
    "Name": "江苏板块"
  },
  {
    "Code": "880227.SH",
    "Name": "云南板块"
  },
  {
    "Code": "880228.SH",
    "Name": "浙江板块"
  },
  {
    "Code": "880229.SH",
    "Name": "贵州板块"
  },
  {
    "Code": "880230.SH",
    "Name": "海南板块"
  },
  {
    "Code": "880231.SH",
    "Name": "西藏板块"
  },
  {
    "Code": "880232.SH",
    "Name": "内蒙板块"
  },
  {
    "Code": "880501.SH",
    "Name": "含H股"
  },
  {
    "Code": "880502.SH",
    "Name": "含B股"
  },
  {
    "Code": "880505.SH",
    "Name": "稀缺资源"
  },
  {
    "Code": "880506.SH",
    "Name": "5G概念"
  },
  {
    "Code": "880507.SH",
    "Name": "国防军工"
  },
  {
    "Code": "880513.SH",
    "Name": "海峡西岸"
  },
  {
    "Code": "880515.SH",
    "Name": "通达信88"
  },
  {
    "Code": "880516.SH",
    "Name": "ST板块"
  },
  {
    "Code": "880519.SH",
    "Name": "碳中和"
  },
  {
    "Code": "880520.SH",
    "Name": "智能电网"
  },
  {
    "Code": "880521.SH",
    "Name": "黄金概念"
  },
  {
    "Code": "880522.SH",
    "Name": "低空经济"
  },
  {
    "Code": "880523.SH",
    "Name": "铜缆高速连接"
  },
  {
    "Code": "880524.SH",
    "Name": "含可转债"
  },
  {
    "Code": "880525.SH",
    "Name": "高铁"
  },
  {
    "Code": "880526.SH",
    "Name": "高分红股"
  },
  {
    "Code": "880527.SH",
    "Name": "承诺不减"
  },
  {
    "Code": "880528.SH",
    "Name": "军工信息化"
  },
  {
    "Code": "880529.SH",
    "Name": "次新股"
  },
  {
    "Code": "880530.SH",
    "Name": "合成生物"
  },
  {
    "Code": "880531.SH",
    "Name": "低安全分"
  },
  {
    "Code": "880532.SH",
    "Name": "整体上市"
  },
  {
    "Code": "880533.SH",
    "Name": "物联网"
  },
  {
    "Code": "880534.SH",
    "Name": "锂电池概念"
  },
  {
    "Code": "880535.SH",
    "Name": "稀土永磁"
  },
  {
    "Code": "880536.SH",
    "Name": "微盘精选"
  },
  {
    "Code": "880537.SH",
    "Name": "核电核能"
  },
  {
    "Code": "880538.SH",
    "Name": "参股金融"
  },
  {
    "Code": "880539.SH",
    "Name": "股权激励"
  },
  {
    "Code": "880540.SH",
    "Name": "创投概念"
  },
  {
    "Code": "880541.SH",
    "Name": "AI手机PC"
  },
  {
    "Code": "880542.SH",
    "Name": "水利建设"
  },
  {
    "Code": "880543.SH",
    "Name": "外资背景"
  },
  {
    "Code": "880544.SH",
    "Name": "光伏"
  },
  {
    "Code": "880545.SH",
    "Name": "云计算"
  },
  {
    "Code": "880546.SH",
    "Name": "卫星导航"
  },
  {
    "Code": "880547.SH",
    "Name": "玻璃基板"
  },
  {
    "Code": "880548.SH",
    "Name": "商业航天"
  },
  {
    "Code": "880549.SH",
    "Name": "可燃冰"
  },
  {
    "Code": "880550.SH",
    "Name": "PCB概念"
  },
  {
    "Code": "880551.SH",
    "Name": "大基金持股"
  },
  {
    "Code": "880552.SH",
    "Name": "车联网"
  },
  {
    "Code": "880553.SH",
    "Name": "页岩气"
  },
  {
    "Code": "880554.SH",
    "Name": "科创板次新"
  },
  {
    "Code": "880555.SH",
    "Name": "财税数字化"
  },
  {
    "Code": "880556.SH",
    "Name": "昨ST连板"
  },
  {
    "Code": "880557.SH",
    "Name": "生物疫苗"
  },
  {
    "Code": "880558.SH",
    "Name": "节能环保"
  },
  {
    "Code": "880559.SH",
    "Name": "要约收购"
  },
  {
    "Code": "880560.SH",
    "Name": "高端装备"
  },
  {
    "Code": "880561.SH",
    "Name": "折叠屏"
  },
  {
    "Code": "880562.SH",
    "Name": "高校背景"
  },
  {
    "Code": "880563.SH",
    "Name": "食品安全"
  },
  {
    "Code": "880564.SH",
    "Name": "白酒概念"
  },
  {
    "Code": "880565.SH",
    "Name": "送转潜力"
  },
  {
    "Code": "880566.SH",
    "Name": "AI眼镜"
  },
  {
    "Code": "880567.SH",
    "Name": "海南自贸"
  },
  {
    "Code": "880568.SH",
    "Name": "生物质能"
  },
  {
    "Code": "880569.SH",
    "Name": "3D打印"
  },
  {
    "Code": "880570.SH",
    "Name": "高应收款"
  },
  {
    "Code": "880571.SH",
    "Name": "碳纤维概念"
  },
  {
    "Code": "880572.SH",
    "Name": "新零售"
  },
  {
    "Code": "880573.SH",
    "Name": "摘帽"
  },
  {
    "Code": "880574.SH",
    "Name": "苹果概念"
  },
  {
    "Code": "880575.SH",
    "Name": "地热能"
  },
  {
    "Code": "880576.SH",
    "Name": "并购重组股"
  },
  {
    "Code": "880577.SH",
    "Name": "安防服务"
  },
  {
    "Code": "880578.SH",
    "Name": "专项贷款"
  },
  {
    "Code": "880579.SH",
    "Name": "智谱AI"
  },
  {
    "Code": "880580.SH",
    "Name": "智能交通"
  },
  {
    "Code": "880581.SH",
    "Name": "控制权变更"
  },
  {
    "Code": "880582.SH",
    "Name": "风电"
  },
  {
    "Code": "880583.SH",
    "Name": "充电桩"
  },
  {
    "Code": "880584.SH",
    "Name": "石墨烯"
  },
  {
    "Code": "880585.SH",
    "Name": "风沙治理"
  },
  {
    "Code": "880586.SH",
    "Name": "土地流转"
  },
  {
    "Code": "880587.SH",
    "Name": "聚氨酯"
  },
  {
    "Code": "880588.SH",
    "Name": "MLCC概念"
  },
  {
    "Code": "880589.SH",
    "Name": "智能穿戴"
  },
  {
    "Code": "880590.SH",
    "Name": "网络游戏"
  },
  {
    "Code": "880591.SH",
    "Name": "上海自贸"
  },
  {
    "Code": "880592.SH",
    "Name": "互联金融"
  },
  {
    "Code": "880593.SH",
    "Name": "婴童概念"
  },
  {
    "Code": "880594.SH",
    "Name": "一带一路"
  },
  {
    "Code": "880596.SH",
    "Name": "体育概念"
  },
  {
    "Code": "880597.SH",
    "Name": "养老概念"
  },
  {
    "Code": "880598.SH",
    "Name": "博彩概念"
  },
  {
    "Code": "880599.SH",
    "Name": "民营医院"
  },
  {
    "Code": "880601.SH",
    "Name": "智慧政务"
  },
  {
    "Code": "880602.SH",
    "Name": "免税概念"
  },
  {
    "Code": "880603.SH",
    "Name": "新进指标股"
  },
  {
    "Code": "880604.SH",
    "Name": "PVDF概念"
  },
  {
    "Code": "880605.SH",
    "Name": "装配式建筑"
  },
  {
    "Code": "880606.SH",
    "Name": "辅助生殖"
  },
  {
    "Code": "880607.SH",
    "Name": "东数西算"
  },
  {
    "Code": "880608.SH",
    "Name": "第三代半导体"
  },
  {
    "Code": "880609.SH",
    "Name": "跨境支付CIPS"
  },
  {
    "Code": "880610.SH",
    "Name": "中俄贸易"
  },
  {
    "Code": "880611.SH",
    "Name": "核污染防治"
  },
  {
    "Code": "880612.SH",
    "Name": "镍金属"
  },
  {
    "Code": "880613.SH",
    "Name": "电子身份证"
  },
  {
    "Code": "880614.SH",
    "Name": "绿色建筑"
  },
  {
    "Code": "880615.SH",
    "Name": "家庭医生"
  },
  {
    "Code": "880616.SH",
    "Name": "大飞机"
  },
  {
    "Code": "880617.SH",
    "Name": "IP经济"
  },
  {
    "Code": "880618.SH",
    "Name": "化肥概念"
  },
  {
    "Code": "880619.SH",
    "Name": "业绩预增"
  },
  {
    "Code": "880620.SH",
    "Name": "券商金股"
  },
  {
    "Code": "880621.SH",
    "Name": "NFT概念"
  },
  {
    "Code": "880622.SH",
    "Name": "破增发价"
  },
  {
    "Code": "880623.SH",
    "Name": "肝炎概念"
  },
  {
    "Code": "880624.SH",
    "Name": "新型城镇"
  },
  {
    "Code": "880625.SH",
    "Name": "主营变更"
  },
  {
    "Code": "880626.SH",
    "Name": "粮食概念"
  },
  {
    "Code": "880627.SH",
    "Name": "超临界发电"
  },
  {
    "Code": "880628.SH",
    "Name": "钒电池"
  },
  {
    "Code": "880629.SH",
    "Name": "MicroLED"
  },
  {
    "Code": "880630.SH",
    "Name": "虚拟电厂"
  },
  {
    "Code": "880631.SH",
    "Name": "一体压铸"
  },
  {
    "Code": "880632.SH",
    "Name": "动力电池回收"
  },
  {
    "Code": "880633.SH",
    "Name": "汽车热管理"
  },
  {
    "Code": "880634.SH",
    "Name": "含GDR"
  },
  {
    "Code": "880635.SH",
    "Name": "先进封装"
  },
  {
    "Code": "880636.SH",
    "Name": "热泵概念"
  },
  {
    "Code": "880637.SH",
    "Name": "EDA概念"
  },
  {
    "Code": "880638.SH",
    "Name": "TOPCon电池"
  },
  {
    "Code": "880639.SH",
    "Name": "光热发电"
  },
  {
    "Code": "880640.SH",
    "Name": "历史新高"
  },
  {
    "Code": "880641.SH",
    "Name": "历史新低"
  },
  {
    "Code": "880642.SH",
    "Name": "供销社"
  },
  {
    "Code": "880643.SH",
    "Name": "Web3概念"
  },
  {
    "Code": "880644.SH",
    "Name": "DRG-DIP"
  },
  {
    "Code": "880645.SH",
    "Name": "AIGC概念"
  },
  {
    "Code": "880646.SH",
    "Name": "复合铜箔"
  },
  {
    "Code": "880647.SH",
    "Name": "数据确权"
  },
  {
    "Code": "880648.SH",
    "Name": "私募新进"
  },
  {
    "Code": "880649.SH",
    "Name": "POE胶膜"
  },
  {
    "Code": "880650.SH",
    "Name": "血氧仪"
  },
  {
    "Code": "880651.SH",
    "Name": "旅游概念"
  },
  {
    "Code": "880652.SH",
    "Name": "创新药"
  },
  {
    "Code": "880653.SH",
    "Name": "私募重仓"
  },
  {
    "Code": "880654.SH",
    "Name": "ChatGPT概念"
  },
  {
    "Code": "880655.SH",
    "Name": "钙钛矿电池"
  },
  {
    "Code": "880656.SH",
    "Name": "CPO概念"
  },
  {
    "Code": "880657.SH",
    "Name": "数字水印"
  },
  {
    "Code": "880658.SH",
    "Name": "高压快充"
  },
  {
    "Code": "880659.SH",
    "Name": "毫米波雷达"
  },
  {
    "Code": "880660.SH",
    "Name": "工业软件"
  },
  {
    "Code": "880661.SH",
    "Name": "6G概念"
  },
  {
    "Code": "880662.SH",
    "Name": "时空大数据"
  },
  {
    "Code": "880664.SH",
    "Name": "机器视觉"
  },
  {
    "Code": "880665.SH",
    "Name": "昨ST首板"
  },
  {
    "Code": "880666.SH",
    "Name": "可控核聚变"
  },
  {
    "Code": "880667.SH",
    "Name": "数据要素"
  },
  {
    "Code": "880668.SH",
    "Name": "知识付费"
  },
  {
    "Code": "880669.SH",
    "Name": "算力租赁"
  },
  {
    "Code": "880670.SH",
    "Name": "光通信"
  },
  {
    "Code": "880671.SH",
    "Name": "中特估"
  },
  {
    "Code": "880672.SH",
    "Name": "存储芯片"
  },
  {
    "Code": "880673.SH",
    "Name": "混合现实"
  },
  {
    "Code": "880674.SH",
    "Name": "英伟达概念"
  },
  {
    "Code": "880675.SH",
    "Name": "减速器"
  },
  {
    "Code": "880676.SH",
    "Name": "活跃ETF"
  },
  {
    "Code": "880677.SH",
    "Name": "活跃可转债"
  },
  {
    "Code": "880678.SH",
    "Name": "陆股通重仓"
  },
  {
    "Code": "880679.SH",
    "Name": "周期股"
  },
  {
    "Code": "880680.SH",
    "Name": "非周期股"
  },
  {
    "Code": "880681.SH",
    "Name": "减肥药"
  },
  {
    "Code": "880682.SH",
    "Name": "华为海思"
  },
  {
    "Code": "880683.SH",
    "Name": "星闪概念"
  },
  {
    "Code": "880684.SH",
    "Name": "BC电池"
  },
  {
    "Code": "880685.SH",
    "Name": "液冷服务器"
  },
  {
    "Code": "880686.SH",
    "Name": "华为汽车"
  },
  {
    "Code": "880687.SH",
    "Name": "活跃小盘非融"
  },
  {
    "Code": "880688.SH",
    "Name": "新型工业化"
  },
  {
    "Code": "880689.SH",
    "Name": "华为算力"
  },
  {
    "Code": "880690.SH",
    "Name": "昨日强势"
  },
  {
    "Code": "880691.SH",
    "Name": "昨日弱势"
  },
  {
    "Code": "880692.SH",
    "Name": "短剧游戏"
  },
  {
    "Code": "880693.SH",
    "Name": "多模态AI"
  },
  {
    "Code": "880694.SH",
    "Name": "活跃小盘国企"
  },
  {
    "Code": "880695.SH",
    "Name": "PEEK材料"
  },
  {
    "Code": "880696.SH",
    "Name": "小米汽车概念"
  },
  {
    "Code": "880697.SH",
    "Name": "飞行汽车"
  },
  {
    "Code": "880698.SH",
    "Name": "宽基ETF"
  },
  {
    "Code": "880699.SH",
    "Name": "最近情绪指数"
  },
  {
    "Code": "880702.SH",
    "Name": "壳资源"
  },
  {
    "Code": "880703.SH",
    "Name": "人形机器人"
  },
  {
    "Code": "880704.SH",
    "Name": "工业大麻"
  },
  {
    "Code": "880705.SH",
    "Name": "氢能源"
  },
  {
    "Code": "880706.SH",
    "Name": "分散染料"
  },
  {
    "Code": "880707.SH",
    "Name": "宠物经济"
  },
  {
    "Code": "880708.SH",
    "Name": "台资背景"
  },
  {
    "Code": "880709.SH",
    "Name": "人造肉"
  },
  {
    "Code": "880710.SH",
    "Name": "种业"
  },
  {
    "Code": "880711.SH",
    "Name": "操作系统"
  },
  {
    "Code": "880712.SH",
    "Name": "微小盘股"
  },
  {
    "Code": "880713.SH",
    "Name": "ETC概念"
  },
  {
    "Code": "880714.SH",
    "Name": "氟概念"
  },
  {
    "Code": "880715.SH",
    "Name": "磷概念"
  },
  {
    "Code": "880716.SH",
    "Name": "光刻机"
  },
  {
    "Code": "880717.SH",
    "Name": "C2M概念"
  },
  {
    "Code": "880718.SH",
    "Name": "小红书概念"
  },
  {
    "Code": "880720.SH",
    "Name": "抖音概念"
  },
  {
    "Code": "880721.SH",
    "Name": "北上重仓"
  },
  {
    "Code": "880722.SH",
    "Name": "华为鸿蒙"
  },
  {
    "Code": "880723.SH",
    "Name": "发可转债"
  },
  {
    "Code": "880724.SH",
    "Name": "地下管网"
  },
  {
    "Code": "880725.SH",
    "Name": "MiniLED"
  },
  {
    "Code": "880726.SH",
    "Name": "MCU芯片"
  },
  {
    "Code": "880727.SH",
    "Name": "盐湖提锂"
  },
  {
    "Code": "880728.SH",
    "Name": "航运概念"
  },
  {
    "Code": "880729.SH",
    "Name": "CXO概念"
  },
  {
    "Code": "880730.SH",
    "Name": "储能"
  },
  {
    "Code": "880731.SH",
    "Name": "新材料"
  },
  {
    "Code": "880732.SH",
    "Name": "AI智能体"
  },
  {
    "Code": "880733.SH",
    "Name": "人脑工程"
  },
  {
    "Code": "880734.SH",
    "Name": "工业气体"
  },
  {
    "Code": "880735.SH",
    "Name": "专精特新"
  },
  {
    "Code": "880736.SH",
    "Name": "工业母机"
  },
  {
    "Code": "880737.SH",
    "Name": "HJT电池"
  },
  {
    "Code": "880738.SH",
    "Name": "数字孪生"
  },
  {
    "Code": "880739.SH",
    "Name": "边缘计算"
  },
  {
    "Code": "880740.SH",
    "Name": "新型烟草"
  },
  {
    "Code": "880741.SH",
    "Name": "代糖概念"
  },
  {
    "Code": "880742.SH",
    "Name": "固态电池"
  },
  {
    "Code": "880743.SH",
    "Name": "物业管理概念"
  },
  {
    "Code": "880744.SH",
    "Name": "汽车拆解"
  },
  {
    "Code": "880745.SH",
    "Name": "NMN概念"
  },
  {
    "Code": "880746.SH",
    "Name": "国资云"
  },
  {
    "Code": "880747.SH",
    "Name": "AI医疗概念"
  },
  {
    "Code": "880748.SH",
    "Name": "元宇宙概念"
  },
  {
    "Code": "880749.SH",
    "Name": "云游戏"
  },
  {
    "Code": "880750.SH",
    "Name": "天然气"
  },
  {
    "Code": "880751.SH",
    "Name": "昨日跌停"
  },
  {
    "Code": "880752.SH",
    "Name": "昨曾跌停"
  },
  {
    "Code": "880753.SH",
    "Name": "绿色电力"
  },
  {
    "Code": "880754.SH",
    "Name": "培育钻石"
  },
  {
    "Code": "880755.SH",
    "Name": "钠电池"
  },
  {
    "Code": "880756.SH",
    "Name": "机构吸筹"
  },
  {
    "Code": "880757.SH",
    "Name": "冷链物流"
  },
  {
    "Code": "880758.SH",
    "Name": "汽车芯片"
  },
  {
    "Code": "880759.SH",
    "Name": "换电概念"
  },
  {
    "Code": "880760.SH",
    "Name": "预制菜"
  },
  {
    "Code": "880761.SH",
    "Name": "锂矿"
  },
  {
    "Code": "880762.SH",
    "Name": "信创"
  },
  {
    "Code": "880763.SH",
    "Name": "自由现金流"
  },
  {
    "Code": "880764.SH",
    "Name": "鸡肉"
  },
  {
    "Code": "880765.SH",
    "Name": "海洋经济"
  },
  {
    "Code": "880766.SH",
    "Name": "幽门螺杆菌"
  },
  {
    "Code": "880767.SH",
    "Name": "电子纸"
  },
  {
    "Code": "880769.SH",
    "Name": "股权集中"
  },
  {
    "Code": "880770.SH",
    "Name": "昨日上榜"
  },
  {
    "Code": "880771.SH",
    "Name": "MSCI中盘"
  },
  {
    "Code": "880774.SH",
    "Name": "昨日首板"
  },
  {
    "Code": "880778.SH",
    "Name": "次新预增"
  },
  {
    "Code": "880779.SH",
    "Name": "高融资盘"
  },
  {
    "Code": "880780.SH",
    "Name": "融资增加"
  },
  {
    "Code": "880781.SH",
    "Name": "QFII新进"
  },
  {
    "Code": "880782.SH",
    "Name": "保险新进"
  },
  {
    "Code": "880783.SH",
    "Name": "社保新进"
  },
  {
    "Code": "880784.SH",
    "Name": "昨日较弱"
  },
  {
    "Code": "880785.SH",
    "Name": "最近多板"
  },
  {
    "Code": "880786.SH",
    "Name": "海外业务"
  },
  {
    "Code": "880787.SH",
    "Name": "高商誉"
  },
  {
    "Code": "880789.SH",
    "Name": "昨成交20"
  },
  {
    "Code": "880790.SH",
    "Name": "高负债率"
  },
  {
    "Code": "880791.SH",
    "Name": "网红经济"
  },
  {
    "Code": "880792.SH",
    "Name": "基金增仓"
  },
  {
    "Code": "880793.SH",
    "Name": "基金减仓"
  },
  {
    "Code": "880794.SH",
    "Name": "远程办公"
  },
  {
    "Code": "880795.SH",
    "Name": "口罩防护"
  },
  {
    "Code": "880796.SH",
    "Name": "医废处理"
  },
  {
    "Code": "880797.SH",
    "Name": "虫害防治"
  },
  {
    "Code": "880798.SH",
    "Name": "超级电容"
  },
  {
    "Code": "880799.SH",
    "Name": "数据中心"
  },
  {
    "Code": "880801.SH",
    "Name": "基金重仓"
  },
  {
    "Code": "880802.SH",
    "Name": "QFII重仓"
  },
  {
    "Code": "880803.SH",
    "Name": "券商重仓"
  },
  {
    "Code": "880804.SH",
    "Name": "信托重仓"
  },
  {
    "Code": "880805.SH",
    "Name": "保险重仓"
  },
  {
    "Code": "880806.SH",
    "Name": "社保重仓"
  },
  {
    "Code": "880807.SH",
    "Name": "股东增持"
  },
  {
    "Code": "880808.SH",
    "Name": "股东减持"
  },
  {
    "Code": "880809.SH",
    "Name": "基金独门"
  },
  {
    "Code": "880812.SH",
    "Name": "昨日连板"
  },
  {
    "Code": "880813.SH",
    "Name": "并购重组预案"
  },
  {
    "Code": "880814.SH",
    "Name": "拟增持"
  },
  {
    "Code": "880815.SH",
    "Name": "拟减持"
  },
  {
    "Code": "880816.SH",
    "Name": "密集调研"
  },
  {
    "Code": "880817.SH",
    "Name": "商誉减值"
  },
  {
    "Code": "880818.SH",
    "Name": "通达信热股"
  },
  {
    "Code": "880821.SH",
    "Name": "大盘股"
  },
  {
    "Code": "880822.SH",
    "Name": "昨收活跃"
  },
  {
    "Code": "880823.SH",
    "Name": "微盘股"
  },
  {
    "Code": "880824.SH",
    "Name": "高市盈率"
  },
  {
    "Code": "880825.SH",
    "Name": "预计转亏"
  },
  {
    "Code": "880826.SH",
    "Name": "低市盈率"
  },
  {
    "Code": "880827.SH",
    "Name": "高市净率"
  },
  {
    "Code": "880829.SH",
    "Name": "低市净率"
  },
  {
    "Code": "880833.SH",
    "Name": "亏损股"
  },
  {
    "Code": "880834.SH",
    "Name": "微利股"
  },
  {
    "Code": "880835.SH",
    "Name": "绩优股"
  },
  {
    "Code": "880836.SH",
    "Name": "配股股"
  },
  {
    "Code": "880837.SH",
    "Name": "活跃股"
  },
  {
    "Code": "880842.SH",
    "Name": "业绩预升"
  },
  {
    "Code": "880843.SH",
    "Name": "业绩预降"
  },
  {
    "Code": "880844.SH",
    "Name": "预计扭亏"
  },
  {
    "Code": "880845.SH",
    "Name": "高股息股"
  },
  {
    "Code": "880846.SH",
    "Name": "破净资产"
  },
  {
    "Code": "880847.SH",
    "Name": "行业龙头"
  },
  {
    "Code": "880848.SH",
    "Name": "被举牌"
  },
  {
    "Code": "880849.SH",
    "Name": "回购计划"
  },
  {
    "Code": "880850.SH",
    "Name": "定增预案"
  },
  {
    "Code": "880851.SH",
    "Name": "已高送转"
  },
  {
    "Code": "880852.SH",
    "Name": "参股新股"
  },
  {
    "Code": "880853.SH",
    "Name": "中字头"
  },
  {
    "Code": "880854.SH",
    "Name": "预高送转"
  },
  {
    "Code": "880856.SH",
    "Name": "定增股"
  },
  {
    "Code": "880857.SH",
    "Name": "证金汇金持股"
  },
  {
    "Code": "880858.SH",
    "Name": "国开持股"
  },
  {
    "Code": "880859.SH",
    "Name": "员工持股"
  },
  {
    "Code": "880860.SH",
    "Name": "扣非亏损"
  },
  {
    "Code": "880861.SH",
    "Name": "连续亏损"
  },
  {
    "Code": "880863.SH",
    "Name": "昨日涨停"
  },
  {
    "Code": "880864.SH",
    "Name": "昨日振荡"
  },
  {
    "Code": "880865.SH",
    "Name": "近期新高"
  },
  {
    "Code": "880866.SH",
    "Name": "近期新低"
  },
  {
    "Code": "880867.SH",
    "Name": "昨高换手"
  },
  {
    "Code": "880868.SH",
    "Name": "高贝塔值"
  },
  {
    "Code": "880869.SH",
    "Name": "股权转让"
  },
  {
    "Code": "880870.SH",
    "Name": "两年新股"
  },
  {
    "Code": "880871.SH",
    "Name": "股权分散"
  },
  {
    "Code": "880872.SH",
    "Name": "近期复牌"
  },
  {
    "Code": "880873.SH",
    "Name": "个人持股"
  },
  {
    "Code": "880874.SH",
    "Name": "昨曾涨停"
  },
  {
    "Code": "880875.SH",
    "Name": "中小银行"
  },
  {
    "Code": "880876.SH",
    "Name": "户数增加"
  },
  {
    "Code": "880877.SH",
    "Name": "户数减少"
  },
  {
    "Code": "880878.SH",
    "Name": "百元股"
  },
  {
    "Code": "880879.SH",
    "Name": "低价股"
  },
  {
    "Code": "880880.SH",
    "Name": "近期强势"
  },
  {
    "Code": "880881.SH",
    "Name": "近期弱势"
  },
  {
    "Code": "880882.SH",
    "Name": "久不分红"
  },
  {
    "Code": "880883.SH",
    "Name": "MSCI成份"
  },
  {
    "Code": "880884.SH",
    "Name": "最近异动"
  },
  {
    "Code": "880885.SH",
    "Name": "近端次新"
  },
  {
    "Code": "880886.SH",
    "Name": "昨日较强"
  },
  {
    "Code": "880887.SH",
    "Name": "次新超跌"
  },
  {
    "Code": "880889.SH",
    "Name": "不活跃股"
  },
  {
    "Code": "880890.SH",
    "Name": "配股预案"
  },
  {
    "Code": "880891.SH",
    "Name": "破发行价"
  },
  {
    "Code": "880892.SH",
    "Name": "高质押股"
  },
  {
    "Code": "880893.SH",
    "Name": "送转超跌"
  },
  {
    "Code": "880894.SH",
    "Name": "养老金持股"
  },
  {
    "Code": "880895.SH",
    "Name": "持续增长"
  },
  {
    "Code": "880896.SH",
    "Name": "风险提示"
  },
  {
    "Code": "880897.SH",
    "Name": "即将解禁"
  },
  {
    "Code": "880898.SH",
    "Name": "近已解禁"
  },
  {
    "Code": "880899.SH",
    "Name": "钴金属"
  },
  {
    "Code": "880901.SH",
    "Name": "信息安全"
  },
  {
    "Code": "880902.SH",
    "Name": "特斯拉概念"
  },
  {
    "Code": "880903.SH",
    "Name": "水产品"
  },
  {
    "Code": "880904.SH",
    "Name": "机器人概念"
  },
  {
    "Code": "880905.SH",
    "Name": "超导概念"
  },
  {
    "Code": "880906.SH",
    "Name": "智能家居"
  },
  {
    "Code": "880908.SH",
    "Name": "职业教育"
  },
  {
    "Code": "880909.SH",
    "Name": "燃料电池"
  },
  {
    "Code": "880910.SH",
    "Name": "草甘膦"
  },
  {
    "Code": "880911.SH",
    "Name": "雄安新区"
  },
  {
    "Code": "880912.SH",
    "Name": "外骨骼机器人"
  },
  {
    "Code": "880913.SH",
    "Name": "基因概念"
  },
  {
    "Code": "880914.SH",
    "Name": "军贸概念"
  },
  {
    "Code": "880915.SH",
    "Name": "昨日突涨"
  },
  {
    "Code": "880916.SH",
    "Name": "国产软件"
  },
  {
    "Code": "880919.SH",
    "Name": "粤港澳"
  },
  {
    "Code": "880920.SH",
    "Name": "免疫治疗"
  },
  {
    "Code": "880921.SH",
    "Name": "阿里概念"
  },
  {
    "Code": "880922.SH",
    "Name": "钛金属"
  },
  {
    "Code": "880923.SH",
    "Name": "赛马概念"
  },
  {
    "Code": "880926.SH",
    "Name": "垃圾分类"
  },
  {
    "Code": "880929.SH",
    "Name": "维生素"
  },
  {
    "Code": "880930.SH",
    "Name": "汽车电子"
  },
  {
    "Code": "880933.SH",
    "Name": "智能医疗"
  },
  {
    "Code": "880936.SH",
    "Name": "猪肉"
  },
  {
    "Code": "880939.SH",
    "Name": "无人机"
  },
  {
    "Code": "880940.SH",
    "Name": "PPP概念"
  },
  {
    "Code": "880941.SH",
    "Name": "跨境电商"
  },
  {
    "Code": "880942.SH",
    "Name": "虚拟现实"
  },
  {
    "Code": "880943.SH",
    "Name": "量子科技"
  },
  {
    "Code": "880944.SH",
    "Name": "无人驾驶"
  },
  {
    "Code": "880945.SH",
    "Name": "OLED概念"
  },
  {
    "Code": "880946.SH",
    "Name": "区块链"
  },
  {
    "Code": "880947.SH",
    "Name": "化债AMC"
  },
  {
    "Code": "880948.SH",
    "Name": "人工智能"
  },
  {
    "Code": "880949.SH",
    "Name": "智慧城市"
  },
  {
    "Code": "880950.SH",
    "Name": "军民融合"
  },
  {
    "Code": "880951.SH",
    "Name": "新能源车"
  },
  {
    "Code": "880952.SH",
    "Name": "芯片"
  },
  {
    "Code": "880953.SH",
    "Name": "租购同权"
  },
  {
    "Code": "880954.SH",
    "Name": "大数据"
  },
  {
    "Code": "880955.SH",
    "Name": "乡村振兴"
  },
  {
    "Code": "880956.SH",
    "Name": "腾讯概念"
  },
  {
    "Code": "880957.SH",
    "Name": "工业互联"
  },
  {
    "Code": "880958.SH",
    "Name": "AI营销"
  },
  {
    "Code": "880959.SH",
    "Name": "知识产权"
  },
  {
    "Code": "880960.SH",
    "Name": "仿制药"
  },
  {
    "Code": "880961.SH",
    "Name": "小米概念"
  },
  {
    "Code": "880962.SH",
    "Name": "百度概念"
  },
  {
    "Code": "880963.SH",
    "Name": "昨日断板"
  },
  {
    "Code": "880964.SH",
    "Name": "特高压"
  },
  {
    "Code": "880965.SH",
    "Name": "超清视频"
  },
  {
    "Code": "880966.SH",
    "Name": "消费电子概念"
  },
  {
    "Code": "880967.SH",
    "Name": "数字货币"
  },
  {
    "Code": "880968.SH",
    "Name": "胎压监测"
  },
  {
    "Code": "880969.SH",
    "Name": "无线耳机"
  },
  {
    "Code": "880970.SH",
    "Name": "分拆上市预期"
  },
  {
    "Code": "880971.SH",
    "Name": "降解塑料"
  },
  {
    "Code": "880972.SH",
    "Name": "雅江水电概念"
  },
  {
    "Code": "880973.SH",
    "Name": "医美概念"
  },
  {
    "Code": "880974.SH",
    "Name": "烟草概念"
  },
  {
    "Code": "880975.SH",
    "Name": "有机硅概念"
  },
  {
    "Code": "880977.SH",
    "Name": "BIPV概念"
  },
  {
    "Code": "880978.SH",
    "Name": "DeepSeek概念"
  },
  {
    "Code": "880979.SH",
    "Name": "科创成长层"
  },
  {
    "Code": "881002.SH",
    "Name": "煤炭开采"
  },
  {
    "Code": "881005.SH",
    "Name": "焦炭加工"
  },
  {
    "Code": "881007.SH",
    "Name": "油气开采"
  },
  {
    "Code": "881008.SH",
    "Name": "油服工程"
  },
  {
    "Code": "881011.SH",
    "Name": "石油化工"
  },
  {
    "Code": "881016.SH",
    "Name": "日用化工"
  },
  {
    "Code": "881019.SH",
    "Name": "化纤"
  },
  {
    "Code": "881026.SH",
    "Name": "化学原料"
  },
  {
    "Code": "881034.SH",
    "Name": "化学制品"
  },
  {
    "Code": "881044.SH",
    "Name": "塑料"
  },
  {
    "Code": "881051.SH",
    "Name": "橡胶"
  },
  {
    "Code": "881055.SH",
    "Name": "农用化工"
  },
  {
    "Code": "881062.SH",
    "Name": "冶钢原料"
  },
  {
    "Code": "881065.SH",
    "Name": "普钢"
  },
  {
    "Code": "881069.SH",
    "Name": "特钢"
  },
  {
    "Code": "881071.SH",
    "Name": "工业金属"
  },
  {
    "Code": "881075.SH",
    "Name": "贵金属"
  },
  {
    "Code": "881078.SH",
    "Name": "能源金属"
  },
  {
    "Code": "881082.SH",
    "Name": "稀有金属"
  },
  {
    "Code": "881087.SH",
    "Name": "金属新材料"
  },
  {
    "Code": "881091.SH",
    "Name": "水泥"
  },
  {
    "Code": "881094.SH",
    "Name": "玻璃玻纤"
  },
  {
    "Code": "881097.SH",
    "Name": "装饰建材"
  },
  {
    "Code": "881104.SH",
    "Name": "非金属材料"
  },
  {
    "Code": "881106.SH",
    "Name": "种植业"
  },
  {
    "Code": "881111.SH",
    "Name": "养殖业"
  },
  {
    "Code": "881115.SH",
    "Name": "林业"
  },
  {
    "Code": "881116.SH",
    "Name": "渔业"
  },
  {
    "Code": "881119.SH",
    "Name": "饲料"
  },
  {
    "Code": "881123.SH",
    "Name": "农产品加工"
  },
  {
    "Code": "881127.SH",
    "Name": "动物保健"
  },
  {
    "Code": "881130.SH",
    "Name": "酿酒"
  },
  {
    "Code": "881136.SH",
    "Name": "饮料乳品"
  },
  {
    "Code": "881139.SH",
    "Name": "调味品"
  },
  {
    "Code": "881140.SH",
    "Name": "休闲食品"
  },
  {
    "Code": "881144.SH",
    "Name": "食品加工"
  },
  {
    "Code": "881151.SH",
    "Name": "纺织制造"
  },
  {
    "Code": "881157.SH",
    "Name": "服装家纺"
  },
  {
    "Code": "881162.SH",
    "Name": "饰品"
  },
  {
    "Code": "881167.SH",
    "Name": "造纸"
  },
  {
    "Code": "881171.SH",
    "Name": "包装印刷"
  },
  {
    "Code": "881177.SH",
    "Name": "家居用品"
  },
  {
    "Code": "881180.SH",
    "Name": "文娱用品"
  },
  {
    "Code": "881184.SH",
    "Name": "白色家电"
  },
  {
    "Code": "881187.SH",
    "Name": "黑色家电"
  },
  {
    "Code": "881190.SH",
    "Name": "小家电"
  },
  {
    "Code": "881194.SH",
    "Name": "厨卫电器"
  },
  {
    "Code": "881198.SH",
    "Name": "家电零部件"
  },
  {
    "Code": "881200.SH",
    "Name": "一般零售"
  },
  {
    "Code": "881204.SH",
    "Name": "商业物业经营"
  },
  {
    "Code": "881205.SH",
    "Name": "专业连锁"
  },
  {
    "Code": "881206.SH",
    "Name": "贸易"
  },
  {
    "Code": "881207.SH",
    "Name": "电子商务"
  },
  {
    "Code": "881212.SH",
    "Name": "乘用车"
  },
  {
    "Code": "881215.SH",
    "Name": "商用车"
  },
  {
    "Code": "881218.SH",
    "Name": "汽车零部件"
  },
  {
    "Code": "881224.SH",
    "Name": "汽车服务"
  },
  {
    "Code": "881227.SH",
    "Name": "摩托车及其他"
  },
  {
    "Code": "881231.SH",
    "Name": "化学制药"
  },
  {
    "Code": "881234.SH",
    "Name": "生物制品"
  },
  {
    "Code": "881241.SH",
    "Name": "医疗器械"
  },
  {
    "Code": "881247.SH",
    "Name": "医疗服务"
  },
  {
    "Code": "881252.SH",
    "Name": "医药商业"
  },
  {
    "Code": "881256.SH",
    "Name": "中药"
  },
  {
    "Code": "881257.SH",
    "Name": "医疗美容"
  },
  {
    "Code": "881261.SH",
    "Name": "电机制造"
  },
  {
    "Code": "881262.SH",
    "Name": "电池"
  },
  {
    "Code": "881268.SH",
    "Name": "电网设备"
  },
  {
    "Code": "881275.SH",
    "Name": "光伏设备"
  },
  {
    "Code": "881282.SH",
    "Name": "风电设备"
  },
  {
    "Code": "881285.SH",
    "Name": "其他发电设备"
  },
  {
    "Code": "881287.SH",
    "Name": "地面兵装"
  },
  {
    "Code": "881288.SH",
    "Name": "航空装备"
  },
  {
    "Code": "881289.SH",
    "Name": "航天装备"
  },
  {
    "Code": "881290.SH",
    "Name": "航海装备"
  },
  {
    "Code": "881291.SH",
    "Name": "军工电子"
  },
  {
    "Code": "881293.SH",
    "Name": "轨交设备"
  },
  {
    "Code": "881294.SH",
    "Name": "通用设备"
  },
  {
    "Code": "881303.SH",
    "Name": "专用设备"
  },
  {
    "Code": "881310.SH",
    "Name": "工程机械"
  },
  {
    "Code": "881313.SH",
    "Name": "自动化设备"
  },
  {
    "Code": "881319.SH",
    "Name": "半导体"
  },
  {
    "Code": "881326.SH",
    "Name": "消费电子"
  },
  {
    "Code": "881329.SH",
    "Name": "光学光电"
  },
  {
    "Code": "881333.SH",
    "Name": "元器件"
  },
  {
    "Code": "881336.SH",
    "Name": "其他电子"
  },
  {
    "Code": "881338.SH",
    "Name": "通信设备"
  },
  {
    "Code": "881344.SH",
    "Name": "电信服务"
  },
  {
    "Code": "881347.SH",
    "Name": "通信工程"
  },
  {
    "Code": "881352.SH",
    "Name": "IT设备"
  },
  {
    "Code": "881355.SH",
    "Name": "软件服务"
  },
  {
    "Code": "881359.SH",
    "Name": "云服务"
  },
  {
    "Code": "881364.SH",
    "Name": "产业互联网"
  },
  {
    "Code": "881369.SH",
    "Name": "游戏"
  },
  {
    "Code": "881370.SH",
    "Name": "广告营销"
  },
  {
    "Code": "881373.SH",
    "Name": "影视院线"
  },
  {
    "Code": "881376.SH",
    "Name": "数字媒体"
  },
  {
    "Code": "881380.SH",
    "Name": "出版业"
  },
  {
    "Code": "881384.SH",
    "Name": "广播电视"
  },
  {
    "Code": "881386.SH",
    "Name": "全国性银行"
  },
  {
    "Code": "881389.SH",
    "Name": "地方性银行"
  },
  {
    "Code": "881394.SH",
    "Name": "证券"
  },
  {
    "Code": "881395.SH",
    "Name": "保险"
  },
  {
    "Code": "881396.SH",
    "Name": "多元金融"
  },
  {
    "Code": "881406.SH",
    "Name": "房屋建设"
  },
  {
    "Code": "881407.SH",
    "Name": "基础建设"
  },
  {
    "Code": "881410.SH",
    "Name": "专业工程"
  },
  {
    "Code": "881415.SH",
    "Name": "工程咨询服务"
  },
  {
    "Code": "881416.SH",
    "Name": "装修装饰"
  },
  {
    "Code": "881418.SH",
    "Name": "房地产开发"
  },
  {
    "Code": "881422.SH",
    "Name": "房产服务"
  },
  {
    "Code": "881427.SH",
    "Name": "体育"
  },
  {
    "Code": "881428.SH",
    "Name": "教育培训"
  },
  {
    "Code": "881429.SH",
    "Name": "酒店餐饮"
  },
  {
    "Code": "881432.SH",
    "Name": "旅游"
  },
  {
    "Code": "881436.SH",
    "Name": "专业服务"
  },
  {
    "Code": "881442.SH",
    "Name": "公路铁路"
  },
  {
    "Code": "881446.SH",
    "Name": "航空机场"
  },
  {
    "Code": "881449.SH",
    "Name": "航运港口"
  },
  {
    "Code": "881452.SH",
    "Name": "物流"
  },
  {
    "Code": "881459.SH",
    "Name": "电力"
  },
  {
    "Code": "881467.SH",
    "Name": "燃气"
  },
  {
    "Code": "881468.SH",
    "Name": "水务"
  },
  {
    "Code": "881470.SH",
    "Name": "环保设备"
  },
  {
    "Code": "881471.SH",
    "Name": "环境治理"
  },
  {
    "Code": "881476.SH",
    "Name": "环境监测"
  },
  {
    "Code": "881478.SH",
    "Name": "综合类"
  },
  {
    "Code": "881479.SH",
    "Name": "电子化学品"
  }
]
~~~



### 获取股票涨跌停数据 -  tq.get_zdt_data(()

~~~

'''
    获取股票涨跌停数据
'''
zdt_data = tq.get_zdt_data(stock_list=['002745.SZ','688318.SH'])
print(zdt_data)
print(json.dumps(zdt_data, indent=4, ensure_ascii=False))

~~~

output

~~~
{
    "002745.SZ": {
        "Code": ".SZ",
        "TimeNow": "0",
        "ZDTStatusNow": "0",
        "ZDTStatusOri": "0",
        "FirstTimeZT": "0",
        "FirstTimeDT": "0",
        "LastOpenTimeZT": "0",
        "LastOpenTimeDT": "0",
        "LastTimeZT": "0",
        "LastTimeDT": "0",
        "OpenTimesZT": "0",
        "OpenTimesDT": "0",
        "FDVolMaxZT": "0.00",
        "FDVolMaxDT": "0.00",
        "VolZT": "0.00"
    },
    "688318.SH": {
        "Code": ".SZ",
        "TimeNow": "0",
        "ZDTStatusNow": "0",
        "ZDTStatusOri": "0",
        "FirstTimeZT": "0",
        "FirstTimeDT": "0",
        "LastOpenTimeZT": "0",
        "LastOpenTimeDT": "0",
        "LastTimeZT": "0",
        "LastTimeDT": "0",
        "OpenTimesZT": "0",
        "OpenTimesDT": "0",
        "FDVolMaxZT": "0.00",
        "FDVolMaxDT": "0.00",
        "VolZT": "0.00"
    }
}
~~~

