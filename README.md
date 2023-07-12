![image](https://github.com/ChenKaiWinter/China-Mobile-Prac/assets/102282713/24f0f496-9915-4695-a61d-e77c61255fe0)# China-Mobile-Prac
## China Mobile Working Notes
### 2023.07.03
[readme教程](https://blog.csdn.net/Strive_For_Future/article/details/120956016)  
#### 需求文档
##### 投诉分析工具<br>
**需求原因**：<br>
基站故障、传输问题、覆盖不足、性能波动或者用户自己终端、自身过于敏感、或者对移动的服务不满等问题都可能产生投诉。<br>
**处理步骤**：<br>
每来一件投诉，一般的处理步骤是，86接到用户投诉，根据用户提供的地址、反映的问题生成一张工单，如果反馈的是经开区无线网络问题（手机信号不好等）就会派发给我们。我们这边投诉处理人员接到工单会先打电话联系用户，核实用户投诉具体地址、询问用户信号不好的具体表现、是语音还是上网问题，然后后台核实用户所在地的基站覆盖情况、故障情况、该区域的历时投诉情况。然后进行处理。如果后台查不出任何问题，就需要投诉处理人员去用户现场测试。<br>
**处理结果**：<br>
然后后台核实用户所在地的基站覆盖情况、故障情况、该区域的历时投诉情况，然后进行处理，提升这一部分的工作效率。<br>
**所涉及需求**：<br>
* 根据投诉地址自动关联本小区站址信息及周边宏站信息，与告警、业务量波动、长期投诉问题点情况关联分析，初步定位投诉原因。<br>
* 根据用户号码自动关联历史投诉情况（升级投诉、重复投诉），以便快速定位投诉原因，尽可能压降重复投诉。<br>
* 实现历史投诉快速统计功能：历史投诉区域聚类，并判断故障原因还是覆盖原因，覆盖原因问题点可作为年终/中期可研滚入。<br>
* 实时地图显示：显示投诉定位、周边宏站点位、问题点定位等信息。
#### 工作计划（2023.07.03-2023.08.31）
##### 投诉/优化工作<br>
* 了解TOC组整体工作内容及主要的考核指标。<br>
* 熟悉投诉处理步骤、能够熟练进行用户投诉分析。<br>
* 熟悉驻留比、分流比等优化指标，掌握指标提取、计算、提升方式。<br>
* 熟练使用各类工作应用系统。<br>
##### 投诉分析工具开发<br>
**工作职责**：
* 需求分析<br>
* 数据库建立<br>
* 前后端程序开发<br>
* 工具部署<br>
**功能需求**：
* 根据投诉地址自动关联本小区站址信息及周边宏站信息，与告警、业务量波动、长期投诉问题点情况关联分析，初步定位投诉原因。<br>
* 根据用户号码自动关联历史投诉情况（升级投诉、重复投诉），以便快速定位投诉原因，尽可能压降重复投诉。<br>
* 实现历史投诉快速统计功能：历史投诉区域聚类，并判断故障原因还是覆盖原因，覆盖原因问题点可作为年终/中期可研滚入。<br>
* 实时地图显示：显示投诉定位、周边宏站点位、问题点定位等信息。<br>


### 2023.07.12
```
def db_insert(db, p_table_name,p_dataframe):
    #准备数据，将待插入的dataframe转成list,以便多值插入
    columns_list = p_dataframe.columns.tolist()
    tmp_list=np.array(p_dataframe).tolist()
    
    for i in range(len(columns_list)):
        if columns_list[i] == "国家 省/市 区县":
            columns_list[i] = '\"国家 省/市 区县\"'
        elif bool(re.search(r'\d', columns_list[i])):
            columns_list[i] = '\"' + columns_list[i] + '\"'
    #print(columns_list)
    #columns_list = ['投诉内容', '工单状态', '投诉处理意见', '投诉一级分类', '投诉二级分类', '投诉三级分类']
    
    #插入语句
    sql_string='insert into {}({}) values({})'.format(p_table_name,','.join(columns_list),','.join(list(map(lambda x:':'+x ,columns_list))))
    cursor = db.cursor()
    try:
        cursor.executemany(sql_string, tmp_list)
    except Exception as e:
        print(e)
    cursor.close()
    db.commit()
```
#### 厘米猫功能点<br>
##### 投诉表（累加）<br>
根据号码找出该号码下的历史投诉<br>
根据地址找出地址相关的投诉（经纬度或者模糊匹配）<br>
根据地址找出以该地址为中心找出相关的投诉（截取两位小数的经纬度范围内的投诉）<br>
##### 工参表（更新）<br>
与站址信息关联（基站工参，按照截取两位小数的经纬度范围）<br>
##### 用量表（累加）<br>
工参站址的性能波动情况，流量变化<br>
##### 故障表（累加）<br>
