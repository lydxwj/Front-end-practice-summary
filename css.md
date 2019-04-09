# css问题

### 1.a连接href

**a href =" ":**

​	 默认打开的还是当前页面，会刷新一下重新打开。

**a href ="#":**

​	 浏览器地址栏网址后面会多显示1个#。不会刷新页面，会回到页面顶部。点击之后会自动跳转到页面的最上面，因为用了这个方法就相当于点击了一个锚记，但是这个锚记又没写ID，所以就默认跳转到页面顶部。

**a href ="Javascript: void(0) ":**		**a href=“Javascript:;”       a href=“##”**   

​	void是一个操作符，这个操作符指定要计算一个表达式但是不返回值。如果在void中写入0（void(0)），则什么也不执行，从而也就形成了一个空链接。

### 2.文字方向

```css
div{ direction:rtl;}		/*文字从右向左排列，有滚动条时候，滚动条在左侧*/
```
### 3.css3动画播放问题

用类名控制css3动画播放首次可以很好播放，但是重复播放时就会出现不能播放问题，原因是已经有了动画类，需要先去掉动画类，再重新添加，才可以完成动画的重新播放。

## 4.用CSS的font-family属性来定义字体

```
@font-face {
  font-family:'YourWebFontName';
  src:url('YourWebFontName.eot');/* IE9 Compat Modes */
  src:url('YourWebFontName.eot?#iefix')format('embedded-opentype'),/* IE6-IE8 */
  url('YourWebFontName.woff')format('woff'),/* Modern Browsers */
  url('YourWebFontName.ttf')format('truetype'),/* Safari, Android, iOS */
  url('YourWebFontName.svg#YourWebFontName')format('svg');/* Legacy iOS */
}
```

## 5.css字体

| **中文名****** |     **英文名******      |      **Unicode******       |
| :------------: | :---------------------: | :------------------------: |
|                |     **Windows******     |                            |
|     * 宋体     |         SimSun          |         \5B8B\4F53         |
|     * 黑体     |         SimHei          |         \9ED1\4F53         |
|   * 微软雅黑   |     Microsoft YaHei     |    \5FAE\8F6F\96C5\9ED1    |
|   微软正黑体   |   Microsoft JhengHei    | \5FAE\x8F6F\6B63\9ED1\4F53 |
|     新宋体     |         NSimSun         |      \65B0\5B8B\4F53       |
|    新细明体    |        PMingLiU         |    \65B0\7EC6\660E\4F53    |
|     细明体     |         MingLiU         |      \7EC6\660E\4F53       |
|     标楷体     |        DFKai-SB         |      \6807\6977\4F53       |
|      仿宋      |        FangSong         |         \4EFF\5B8B         |
|      楷体      |          KaiTi          |         \6977\4F53         |
|  仿宋_GB2312   |     FangSong_GB2312     |     \4EFF\5B8B_GB2312      |
|  楷体_GB2312   |      KaiTi_GB2312       |     \6977\4F53_GB2312      |
|                |     **Mac OS******      |                            |
|   * 华文细黑   | STHeiti Light [STXihei] |    \534E\6587\7EC6\9ED1    |
|   * 华文黑体   |         STHeiti         |    \534E\6587\9ED1\4F53    |
|    华文楷体    |         STKaiti         |    \534E\6587\6977\4F53    |
|    华文宋体    |         STSong          |    \534E\6587\5B8B\4F53    |
|    华文仿宋    |       STFangsong        |    \534E\6587\4EFF\5B8B    |
|    丽黑 Pro    |    LiHei Pro Medium     |       \4E3D\9ED1 Pro       |
|    丽宋 Pro    |    LiSong Pro Light     |       \4E3D\5B8B Pro       |
|     标楷体     |         BiauKai         |      \6807\6977\4F53       |
|   苹果丽中黑   |  Apple LiGothic Medium  | \82F9\679C\4E3D\4E2D\9ED1  |
|   苹果丽细宋   |   Apple LiSung Light    | \82F9\679C\4E3D\7EC6\5B8B  |
|    华文仿宋    |       STFangsong        |    \534E\6587\4EFF\5B8B    |
|    丽黑 Pro    |    LiHei Pro Medium     |       \4E3D\9ED1 Pro       |
|    丽宋 Pro    |    LiSong Pro Light     |       \4E3D\5B8B Pro       |
|     标楷体     |         BiauKai         |      \6807\6977\4F53       |
|   苹果丽中黑   |  Apple LiGothic Medium  | \82F9\679C\4E3D\4E2D\9ED1  |

