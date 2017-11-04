# wx-scroll
微信小程序上拉加载更多上拉刷新组件


# scroll使用文档



# 1、在.wxml中引入组件

<scroll-view class="scroll_container " scroll-y="true" style="position:absolute; height:70%;bottom:0; width:100%; 
    bindscroll="scroll" bindscrolltolower="lower" bindscrolltoupper="upper" bindtouchstart="start" bindtouchend="end" > 
    <include src="../../component/scroll/scrollHeader.wxml"/> 

    <view style="width:100%;height:100%" bindtouchmove="move">
        <block wx:for="{{words}}">  
            <view >{{item.username}}</view> 
        </block>  
    </view>

<include src="../../component/scroll/scrollFooter.wxml"/>                       
</scroll-view> 

  # 说明：scroll-view 样式可自定义  words为传入的数组，在block中自定义加入代码


# 3、.js中引入组件
var register = require('../../component/scroll/scroll.js');

# 4、在onLoad中注册组件 
  register.register(this);

# 5、在.wxss中引入组件样式
  @import '../../component/scroll/scroll.wxss';



# 6、刷新方法
  refresh: function () {
    this.setData({
      page: 1,
      words: []
    })
    this.doLoadData();
  }
  说明：
    page：设置当前页为1
    words：设置为[]
    doLoadData:为初始化数据方法
  

 # 7、加载更多数据
  loadMore: function () {
    var page = this.data.page;
    this.setData({
      page: ++page
    })
    this.doLoadData();
  }
  说明：设置当前页+1，然后初始化数据
  
 # 8、在初始化方法doLoadData 的complete中
    加入  register.loadFinish(this, true);





