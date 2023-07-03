# China-Mobile-Prac
China Mobile Working Notes

投诉分析工具

基站故障、传输问题、覆盖不足、性能波动或者用户自己终端、自身过于敏感、或者对移动的服务不满等问题都可能产生投诉。

每来一件投诉，一般的处理步骤是，86接到用户投诉，根据用户提供的地址、反映的问题生成一张工单，如果反馈的是经开区无线网络问题（手机信号不好等）就会派发给我们。我们这边投诉处理人员接到工单会，先打电话联系用户，核实用户投诉具体地址、询问用户信号不好的具体表现、是语音还是上网问题。然后后台核实用户所在地的基站覆盖情况、故障情况、该区域的历时投诉情况。然后进行处理。如果后台查不出任何问题，就需要投诉处理人员去用户现场测试。

然后后台核实用户所在地的基站覆盖情况、故障情况、该区域的历时投诉情况。然后进行处理。提升这一部分的工作效率。

所以涉及需求：

（1）根据投诉地址自动关联本小区站址信息及周边宏站信息，与告警、业务量波动、长期投诉问题点情况关联分析，初步定位投诉原因。

（2）根据用户号码自动关联历史投诉情况（升级投诉、重复投诉），以便快速定位投诉原因，尽可能压降重复投诉。

（3）实现历史投诉快速统计功能：历史投诉区域聚类，并判断故障原因还是覆盖原因，覆盖原因问题点可作为年终/中期可研滚入。

（4）实时地图显示：显示投诉定位、周边宏站点位、问题点定位等信息。
