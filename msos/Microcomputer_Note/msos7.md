# msos-前端开发

> 负责人，进击的攻城狮成员--周岭

根据msos-ui**设计实现布局和效果**

由于引入ui框架和效果过多，使用了在线压缩和cdn方式引入代码

#### 在线cdn引入资源css

````css
<!--    修改样式引入开始-->
    <link rel="Bookmark" href="https://codecheng-1305009997.cos.ap-chengdu.myqcloud.com/img/20210604085540.png" type="image/x-icon" />
    <link rel="stylesheet" type="text/css" href="https://cdn.jsdelivr.net/gh/vino1016/cdn@2.44/static/matery/css/VinoAnimation.min.css" />
    <link rel="stylesheet" type="text/css" href="https://cdn.jsdelivr.net/gh/vino1016/cdn@2.40/static/css/blog.min.css" />
    <link rel="stylesheet" type="text/css" href="https://cdn.jsdelivr.net/gh/vino1016/cdn@1.1/static/matery/css/materialize.min.css" />
    <link rel="stylesheet" type="text/css" href="https://cdn.jsdelivr.net/gh/vino1016/cdn@2.66/static/matery/css/matery.min.css" />
    <link rel="preload" as="style" href="https://cdn.bootcdn.net/ajax/libs/font-awesome/5.15.1/css/all.min.css" onload="this.onload=null;this.rel='stylesheet'"/>
    <link rel="stylesheet" type="text/css" href="https://cdn.bootcdn.net/ajax/libs/aos/3.0.0-beta.6/aos.css" />
    <link rel="preconnect" href="https://fonts.gstatic.com" />
    <!--倒计时模块-->
    <link href="https://fonts.googleapis.com/css2?family=Noto+Serif+SC&amp;family=Zhi+Mang+Xing&amp;family=Luckiest+Guy&amp;display=swap" rel="stylesheet" />
    <link rel="preconnect" href="https://fonts.gstatic.com">
    <link href="https://fonts.googleapis.com/css2?family=Noto+Serif+SC:wght@400;500;900&display=swap" rel="stylesheet" media="print" onload="this.media='all'">
    <!--    修改样式引入结束-->
````

### 在线cdn引入资源js

```js
<!--引入的js样式开始-->
<script src="https://cdn.bootcdn.net/ajax/libs/jquery/3.5.0/jquery.min.js"></script>
<script src="https://cdn.jsdelivr.net/gh/vino1016/cdn@1.1/static/matery/js/materialize.min.js"></script>
<script src="https://cdn.jsdelivr.net/gh/vino1016/cdn@2.69/static/matery/js/matery.min.js"></script>
<script async="async" src="https://cdn.jsdelivr.net/gh/vino1016/cdn@2.61/static/js/effect/VinoEffect.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/lazyload@2.0.0-rc.2/lazyload.js"></script>
<script src="https://cdn.bootcdn.net/ajax/libs/typed.js/2.0.11/typed.min.js"></script>
<script src="https://cdn.bootcdn.net/ajax/libs/aos/3.0.0-beta.6/aos.js"></script>
<script async="async" src="https://cdn.bootcdn.net/ajax/libs/instant.page/5.1.0/instantpage.min.js" type="module"></script>
<script src="https://eqcn.ajz.miesnfu.com/wp-content/plugins/wp-3d-pony/live2dw/lib/L2Dwidget.min.js"></script>
<!--引入的js样式结束-->
```



### 首页效果实现`homepage.html`

页眉实现

````html
<!--页眉修改开始-->
<header id="headerV" class="navbar-fixed">
    <nav id="headNav" class="h-color nav-transparent" style="transition: background .6s ease-in-out,padding .6s ease-in-out;">
        <div id="navContainer" class="nav-wrapper container">
            <div class="brand-logo">
                <a href="/" class="waves-effect waves-light">
                    <!--首页左上角logo图片-->
                    <img src="https://codecheng-1305009997.cos.ap-chengdu.myqcloud.com/img/20210604085540.png" class="logo-img" alt="LOGO">

                    <span class="logo-span"></span>
                </a>
                <div id="tp-weather-widget" class="hide-on-med-and-down" style="display:inline-block;font-family:'Noto Serif SC',serif !important;"></div>
            </div>
            <a href="#" data-target="mobile-nav" class="sidenav-trigger button-collapse"><i style="color: #0C0C0C" class="fa fa-bars"></i></a>
            <ul class="right nav-menu">
                <li class="hide-on-med-and-down nav-item">
                    <a href="/homepage" class="waves-effect waves-light Vino-color">
                        <i class="fas fa-home fa-2x" style="zoom: 0.6;"></i>
                        <span>首页</span>
                    </a>
                </li>

                <li class="hide-on-med-and-down nav-item">
                    <a href="/aboutMe" class="waves-effect waves-light Vino-color">
                        <i class="fas fa-address-book fa-2x" style="zoom: 0.6;"></i>
                        <span>关于</span>
                    </a>
                </li>
                <li class="hide-on-med-and-down nav-item">
                    <a href="/link" class="waves-effect waves-light Vino-color">
                        <i class="fas fa-link fa-2x" style="zoom: 0.6;"></i>
                        <span>友链</span>
                    </a>
                </li>
                <li class="hide-on-med-and-down nav-item">
                    <a href="/message" class="waves-effect waves-light Vino-color">
                        <i class="fas fa-comments fa-2x" style="zoom: 0.6;"></i>
                        <span>留言</span>
                    </a>
                </li>
                <li>

                    <!--登录-->
                <li class="hide-on-med-and-down nav-item">
                    <a href="/html/login.html"   class="waves-effect waves-light Vino-color">
                        <i class="fas fa-archive fa-2x" style="zoom: 0.6;"></i>
                        <span>登录</span>
                    </a>


                    <a href="#searchModal" class="modal-trigger waves-effect waves-light Vino-color">
                        <i id="searchIcon" class="fa fa-search fa-2x" title="搜索" style="zoom: 0.85;"></i>
                    </a>
                </li>
                <li class="hide-on-med-and-down">
                    <a onclick="switchNightModeTop()" class="modal-trigger waves-effect waves-light Vino-color">
                        <i class="fa fa-moon" id="changeMode-top"  title="切换主题" style="zoom: 0.85;"></i>
                    </a>
                </li>
            </ul>
            <div id="mobile-nav" class="side-nav sidenav">

                <div class="mobile-head bg-color">

                    <img src="https://codecheng-1305009997.cos.ap-chengdu.myqcloud.com/img/20210604085540.png" class="logo-img circle responsive-img">
                    <div class="logo-name" style="font-family:'Luckiest Guy',cursive">msos</div>
                    <div class="logo-desc">
                        再小的帆也能远航，我们的眼里有星辰大海。
                    </div>
                </div>
                <ul class="menu-list mobile-menu-list">
                    <li class="m-nav-item">
                        <a href="/#" class="waves-effect waves-light">
                            <i class="fas fa-home fa-2x"></i>
                            首页
                        </a>
                    </li>
                    <li class="m-nav-item">
                        <a href="/link" class="waves-effect waves-light">
                            <i class="fas fa-link fa-2x"></i>
                            友链
                        </a>
                    </li>
                    <li class="m-nav-item">
                        <a href="/message" class="waves-effect waves-light">
                            <i class="fas fa-comments fa-2x"></i>
                            留言
                        </a>
                    </li>
                    <!--登录-->
                    <li class="hide-on-med-and-down nav-item">
                        <a href="/html/login.html"   class="waves-effect waves-light Vino-color">
                            <i class="fas fa-archive fa-2x" style="zoom: 0.6;"></i>
                            <span>登录</span>
                        </a>

                    </li>
                    <li class="m-nav-item">
                        <a href="/aboutMe" class="waves-effect waves-light">
                            <i class="fas fa-address-book fa-2x"></i>
                            关于
                        </a>
                    </li>
                </ul>
            </div>
        </div>
    </nav>
</header>
<!--页眉修改结束-->
````

首页封面动画实现

```html
<!--封面吹蜡烛动画开始-->
<div class="bg-cover pd-header article-cover" style="height: 100vh" id="smarts">
    <div class="candle-con">
        <div class="wrapper">
            <div class="candles">
                <div class="light__wave"></div>
                <div class="candle1">
                    <div class="candle1__body">
                        <div class="candle1__eyes">
                            <span class="candle1__eyes-one"></span>
                            <span class="candle1__eyes-two"></span>
                        </div>
                        <div class="candle1__mouth"></div>
                    </div>
                    <div class="candle1__stick"></div>
                </div>
                <div class="candle2">
                    <div class="candle2__body">
                        <div class="candle2__eyes">
                            <div class="candle2__eyes-one"></div>
                            <div class="candle2__eyes-two"></div>
                        </div>
                    </div>
                    <div class="candle2__stick"></div>
                </div>
                <div class="candle2__fire"></div>
                <div class="sparkles-one"></div>
                <div class="sparkles-two"></div>
                <div class="candle__smoke-one">
                </div>
                <div class="candle__smoke-two">
                </div>
            </div>
            <div class="floor">
            </div>
        </div>
    </div>
<!--封面吹蜡烛动画结束-->
```

动画跳动的字

````html
<!--  蜡烛动画里面的字-->
    <div class="workBoy-con">
        <div class="wrapper2">
            <div class="sofa">
                <div class="sofa-cushion"></div>
                <div class="sofa-bottom-l"></div>
                <div class="sofa-bottom-r"></div>
            </div>
        </div>
        <div class="cat-V">
            <div class="cat-arm-shoulder"></div>
            <div class="cat-head">
                <div class="cat-ear-l"></div>
                <div class="cat-ear-r"></div>
                <div class="cat-eye-l"></div>
                <div class="cat-eye-r"></div>
            </div>
            <div class="cat-arm-l"></div>
            <div class="cat-arm-r"></div>
            <div class="cat-tale"></div>
        </div>
        <div class="boy">
            <div class="arm-l"></div>
            <div class="foot-l"></div>
            <div class="head">
                <div class="face">
                    <div class="hair-1"></div>
                    <div class="hair-2"></div>
                    <div class="eye-l"></div>
                    <div class="eye-r"></div>
                </div>
                <div class="hair-3"></div>
            </div>
            <div class="foot-r"></div>
            <div class="arm-r"></div>
            <div class="laptop">
                <div class="light"></div>
            </div>
        </div>
    </div>
    <div data-aos="fade-right" data-aos-delay="1700" class="about-tag-about hide-on-med-and-down">
        <div class="V-title">
            <span>&quot;MSOS论坛&quot;</span>
        </div>
    </div>
    <div data-aos="fade-left" data-aos-delay="1700" class="hide-on-med-and-down">
        <div class="V-title">
            <span class="article-tag-Vino">&quot;DYZZ&quot;</span>
            <span class="about-tag-blog">&quot;Blog&quot;</span>
        </div>
    </div>
    <div class="center-align article-typed" style="top:72vh;">
        <span id="subtitle" style="font-size:28px;color: #28a6de"></span>
    </div>
    <div class="hide-on-med-and-down V-img" data-aos="zoom-in" data-aos-delay="1700">
    </div>
    <div class="hide-on-large-only center-align m-V-img-article" style="width: 100vw" data-aos="zoom-in" data-aos-delay="1700">
        <img src="https://codecheng-1305009997.cos.ap-chengdu.myqcloud.com/img/20210604085540.png" />
        <div class="V-title m-V-title">
            <span>&quot;msos&quot;</span>
        </div>
    </div>

</div>

````

热评设计部分

```html
<!--热评-->
<div class="poem-wrap">
    <div class="poem-border poem-left"></div>
    <div class="poem-border poem-right"></div>
    <h1>MSOS</h1>
    <p id="poem">忘掉生日，忘掉青涩的诗，忘掉他不厌其烦夜夜追逐他影子。</p>
    <p id="info">邱意 · 《 菱形月亮 》</p>
</div>
<script>
    $.get("https://v1.hitokoto.cn?c=d&c=h&c=j",function(o,t){"success"==t?($("#poem").html(o.hitokoto),null!=o.from_who?$("#info").html(o.from_who+" · 《 "+o.from+" 》"):$("#info").html(" “ "+o.from+" ” ")):$("#poem").html("获取出错啦")})
</script>

```

倒计时模块

```html
<body onload="countTime()" id="body">
<!-- 现在时间 -->
<div class="time-now">
    <span id="time-now" onclick="nowtip()">加载中...</span><br>
    <span id="hitokoto" style="display: none;"></span>
</div><br>
<!-- 主体部分描述 -->
<div class="desc">
    <b><span id="yuekao">msos规划</span><br>
        <span class="desc2" id="desc2">倒计时</span></b>

</div>
<!-- 近期倒计时 -->
<div class="time-yk" id="timeyk">
    <b><span id="_d" onclick="tip()">加载中...</span></b>
    <b><span id="_h" onclick="tip()"></span></b>
    <b><span id="_m" onclick="tip()"></span></b>
    <b><span id="_s" onclick="tip()"></span></b>
</div>
<div class="time" id="time">
    <b><span class="desc-qm" id="qimo">期末提交</span></b>
    <b><span class="desc-zk" id="zhongkao">毕业快乐</span></b>
    <b><span class="desc-gk" id="gaokao">msos完善</span><br></b>
    <!-- 期末倒计时 -->
    <div class="time-qm" id="timeqm">
        <b><span id="q_d" onclick="tip()">加载中...</span></b>
        <!-- <b><span id="q_h" onclick="tip()">加载中...</span></b>
    <b><span id="q_m" onclick="tip()">加载中...</span></b>
    <b><span id="q_s" onclick="tip()">加载中...</span></b> -->
    </div>
    <!-- 毕业倒计时 -->
    <div class="time-zk" id="timezk">
        <b><span id="z_d" onclick="tip()">加载中...</span></b>
        <!-- <b><span id="z_h" onclick="tip()">加载中...</span></b>
    <b><span id="z_m" onclick="tip()">加载中...</span></b>
    <b><span id="z_s" onclick="tip()">加载中...</span></b> -->
    </div>
    <!-- msos提交倒计时 -->
    <div class="time-gk" id="timegk">
        <b><span id="g_d" onclick="tip()">加载中...</span></b>

    </div>

</div>
<!--msos倒计时模块结束-->

<br>
```

使用vue实现msos人生清单模式

````html
<!--引入vue-->
<script src="https://cdn.bootcss.com/vue/2.6.10/vue.min.js"></script>
<!--人生清单创意开始-->
<div class="container">
    <div class="card">
        <div class="card-content">
            <div class="tag-title center-align">
                <div class="miaoshus">
                    <div class="title center-align">“ Ticktack 滴滴答答~ ”</div>
                    “ 人生几何，九百月矣，深深的话，浅浅的说 ”
                </div>
                <hr>

                <!-- 计算时间模块 -->
                <div class="wrap">
                    <p>“ 人生只有 900 余月</p>
                    <p>过去的，是回忆</p>
                    <p>淡淡的约定，浅浅的留影 ”</p>
                    <div><canvas class="myLife" width="300px" height="300px"></canvas></div>
                    <p>“ 截至此刻，仅剩 '<span class="im0now"></span><span style="color: #e96900;font-size: 20px;">%</span>' 掌握在自己的手中</p>
                    <p>幸运和安逸还是留给后面的人生吧，我想趁着有梦，豁出一切。 ”</p>
                    <script>
                        var birthday=new Date(2002,5,30);
                        var live=(new Date-birthday)/2592000000;
                        var range=[0,live-1];
                        for(var i=0;30>i;i++){
                            for(var j=0;30>j;j++){
                                var current=30*i+j,
                                    canvas=document.getElementsByClassName("myLife")[0],
                                    ctx=canvas.getContext("2d");
                                current>=range[0]&&current<=range[1]?ctx.fillStyle="#ccc":ctx.fillStyle="#e96900",
                                    ctx.fillRect(10*j+1,10*i+1,8,8),ctx.strokeStyle="#000",
                                    ctx.lineWidth=1,
                                    ctx.strokeRect(10*j,10*i,10,10)}}
                        setInterval(function(){if($("span").hasClass("im0now"))
                            {
                                document.getElementsByClassName("im0now")[0].innerHTML=(100-(new Date-birthday)/2592000000/9).toFixed(9)}}
                            ,300);
                    </script>
                </div>



            </div>


        </div>
    </div>

    <div class="card">
        <div class="card-content">

            <div class="biaotis">
                <span>时间从来不语，只在悄然间流逝。</span>

            </div>

            <div class="de">

                <div class="jt">
                    <div class="dyy">
                        今天
                    </div>
                    <div class="dee">
                        <div class="jdt">
                            <div class="jdt_son" style="width: 52.3414%;">&nbsp;</div>
                        </div>
                    </div>
                    <div class="dss">512%</div>
                </div>

                <div class="bz">
                    <div class="dyy">
                        本周
                    </div>
                    <div class="dee">
                        <div class="jdt">
                            <div class="jdt_son" style="width: 78.9059%;">&nbsp;</div>
                        </div>
                    </div>
                    <div class="dss">79%</div>
                </div>

                <div class="by">
                    <div class="dyy">
                        本月
                    </div>
                    <div class="dee">
                        <div class="jdt">
                            <div class="jdt_son" style="width: 58.5879%;">&nbsp;</div>
                        </div>
                    </div>
                    <div class="dss">59%</div>
                </div>

                <div class="jn">
                    <div class="dyy">
                        今年
                    </div>
                    <div class="dee">
                        <div class="jdt">
                            <div class="jdt_son" style="width: 97.2357%;">&nbsp;</div>
                        </div>
                    </div>
                    <div class="dss">97%</div>
                </div>


            </div>
        </div>


        <script>

            // 人生进度条
            function Progress_time() {
                var mydate = new Date();
                var nian = mydate.getFullYear();
                var yue = mydate.getMonth() + 1;
                var ri = mydate.getDate();

                // 计算出今天的百分比
                var jt_a = ((mydate.getHours() * 3600) + (mydate.getMinutes() * 60) + mydate.getSeconds()) / 864;
                var jt = jt_a + '%';
                $(".jt .dss").text(parseFloat(jt.replace("%", "")).toFixed(0) + '%');

                // 计算出本周的百分比
                var bz = null;
                if (mydate.getDay() == 0) {
                    bz = (6 + jt_a / 100) / 0.07 + '%';
                } else {
                    bz = ((mydate.getDay() - 1) + jt_a / 100) / 0.07 + '%'
                }
                $(".bz .dss").text(parseFloat(bz.replace("%", "")).toFixed(0) + '%');

                // 计算出当月共有多少天（方便下面调用）
                function yue_s(z) {
                    if (z == 1 || z == 3 || z == 5 || z == 7 || z == 8 || z == 10 || z == 12) {
                        return 31;
                    } else if (z != 2) {
                        return 30;
                    } else {
                        if (nian / 4 == 0) {
                            return 29;
                        } else {
                            return 28;
                        }
                    }
                }

                // 计算出本月的百分比
                by = ((ri-1) / yue_s(yue))*100+jt_a/100;
                by_viw = by + '%';
                $(".by .dss").text(parseFloat(by_viw.replace("%", "")).toFixed(0) + '%');

                // 计算出：从今年1月1号，直到现在共有多少天
                var jn = 0;
                var dayue = yue;
                for (i = 1; i < dayue + 1; ++i) {
                    if (i >= 3) {
                        if (i != dayue) {
                            jn = jn + yue_s(i);
                        } else {
                            jn = jn + ri;
                        }
                    } else if (i == 2) {
                        if (i != dayue) {
                            jn = jn + yue_s(2);
                        } else {
                            jn = jn + ri;
                        }
                    } else if (i == 1) {
                        if (i != dayue) {
                            jn = 31;
                        } else {
                            jn = ri;
                        }
                    }
                }

                // 计算出今年的百分比
                var runi = 3.65;
                if (yue_s(2) == 29) {
                    runi = 3.66
                }
                jn = (jn / runi + jt_a / 100) + '%';
                $(".jn .dss").text(parseFloat(jn.replace("%", "")).toFixed(0) + '%');



                // 把上面计算出的数据，展示在页面上
                $(".jt .dee .jdt .jdt_son").animate({
                    width: jt
                }, 2000);

                $(".bz .dee .jdt .jdt_son").animate({
                    width: bz
                }, 2000);

                $(".by .dee .jdt .jdt_son").animate({
                    width: by_viw
                }, 2000);

                $(".jn .dee .jdt .jdt_son").animate({
                    width: jn
                }, 2000);



            }
            Progress_time();



        </script>
        <div class="jzb">
            <div class="clock">
                <div class="hour">
                    <div class="hr"></div>
                </div>

                <div class="min">
                    <div class="mn"></div>
                </div>

                <div class="sec">
                    <div class="sc"></div>
                </div>
            </div>
        </div>

        <script>
            // 获取几个时钟的dom
            let hr = document.querySelector(".hr");
            let mn = document.querySelector(".mn");
            let sc = document.querySelector(".sc");
            let time = document.querySelector(".time_wrap1");
            //根据当前时间初始化表盘时钟
            let date = new Date();
            let hour = date.getHours();
            let min = date.getMinutes();
            let sec = date.getSeconds();
            let n = sec;
            setInterval(() => {
                hour = date.getHours();
                hr.style.transform = `rotateZ(${hour * 30 + min / 2}deg)`;
                mn.style.transform = `rotateZ(${min * 6}deg)`;
                sc.style.transform = `rotateZ(${sec * 6}deg)`;

                n++;
                min = min + parseInt(i / 60);
                sec++;
                if (n === 60) i = 0;

                let startTime = new Date("2019-9-1"); // 开始时间
                let endTime = new Date(); // 结束时间
                let usedTime = endTime - startTime; // 相差的毫秒数
                let days = Math.floor(usedTime / (24 * 3600 * 1000)); // 计算出天数
                let leavel = usedTime % (24 * 3600 * 1000); // 计算天数后剩余的时间
                let hours = Math.floor(leavel / (3600 * 1000)); // 计算剩余的小时数
                let leavel2 = leavel % (3600 * 1000); // 计算剩余小时后剩余的毫秒数
                let minutes = Math.floor(leavel2 / (60 * 1000)); // 计算剩余的分钟数
                let level3 = leavel2 - minutes * 60 * 1000;
                let seconds = Math.floor(level3 / 1000);
            }, 1000);
        </script>

        <br>

        <div class="biaotis">
            <span>距离</span>
            <span class="zhuti">2022</span>
            <span>仅有</span>
        </div>
        <div id="CountMsg" class="HotDate">
            <span id="t_d">00天</span>
            <span id="t_h">00时</span>
            <span id="t_m">00分</span>
            <span id="t_s">00秒</span>
        </div>
        <script type="text/javascript">
            function getRTime(){
                var EndTime = new Date('2022/01/01 00:00:00'); //截止时间
                var NowTime = new Date();
                var t = EndTime.getTime() - NowTime.getTime();

                //累减
                // var d=Math.floor(t/1000/60/60/24);
                // t-=d*(1000*60*60*24);
                // var h=Math.floor(t/1000/60/60);
                // t-=h*60*60*1000;
                // var m=Math.floor(t/1000/60);
                // t-=m*60*1000;
                // var s=Math.floor(t/1000);

                //累加
                var d=Math.floor(t/1000/60/60/24);
                var h=Math.floor(t/1000/60/60%24);
                var m=Math.floor(t/1000/60%60);
                var s=Math.floor(t/1000%60);

                document.getElementById("t_d").innerHTML = d + "天";
                document.getElementById("t_h").innerHTML = h + "时";
                document.getElementById("t_m").innerHTML = m + "分";
                document.getElementById("t_s").innerHTML = s + "秒";
            }
            setInterval(getRTime,1000);
        </script>

    </div>
    <div class="main card">
        <div class="card-content">
            <p class="center">没有目标的人生，亦犹如行尸走肉</p>
            <div class="note info">
                公告：这里可作为各位到访msos博客论坛的一个心愿单模块，<br>
                1. 可以在下方写下自己今年或者近期的愿望或者flag，<br>
                2. 例如留下一个flag到下一年或者下一周再次来打卡，<br>
                3. 欢迎大家来留下自己的todolist哦 ~ ，<br>
                4. 若有什么建议或者问题请来msos主页站点的留言板留言哦~<br>
                (注意：此模块使用localstorage，所以输入的内容只存在于你自己的设备上，其他人访问该网页是看不到你的内容的，私密性强，所以可放心键入清单内容。望周知~ 桌面端体验更佳哦~)
            </div>

            <h3 class="big-title">添加任务：</h3>
            <input
                    placeholder="例如：找到一份工作，学会一首歌。 （提示：回车即可添加任务，双击列表标题即可编辑）"
                    class="task-input"
                    type="text"
                    v-on:keyup.enter="enterFn"
                    v-model="todo"
            />
            <ul class="task-count">
                <li>{{unComplete}}个任务未完成</li>
                <li class="action">
                    <a :class="{active:visibility!=='unCompleted'&&visibility!=='completed'}" href="#all">全部</a>
                    <a :class="{active:visibility==='unCompleted'}" href="#unCompleted">未完成</a>
                    <a :class="{active:visibility==='completed'}" href="#completed">已完成</a>
                </li>
            </ul>
            <h3 class="big-title">任务列表：</h3>
            <div class="tasks">

                <span class="no-task-tip" v-show="!list.length">还没有添加任何任务</span>
                <ul class="todo-list" v-show="list.length">
                    <li class="todo"
                        v-for="item in filterData"
                        v-bind:class="{completed:item.isComplete,editing:item===edtorTodos}"
                    >
                        <div class="view">
                            <input class="toggle"
                                   type="checkbox"
                                   v-model="item.isComplete"
                            />
                            <label @dblclick="edtorTodo(item)">{{item.title}}</label>
                            <button
                                    class="destroy"
                                    @click="delFn(item)"
                            ></button>
                            <i class="fabutime"></i>
                        </div>
                        <input
                                class="edit"
                                type="text"
                                v-focus="edtorTodos===item"
                                v-model="item.title"
                                @blur="edtoEnd(item)"
                                @keyup.enter="edtoEnd(item)"
                                @keyup.esc="cancelEdit(item)"
                        />
                    </li>
                </ul>
            </div>
        </div>
    </div>

    <div class="daodile">呐，已经到底啦，去上方留下自己的todolist吧~</div>
    <!-- <script>
        var date = new Date();
        var fabutime = date.toLocaleString( ); //获取日期与时间
        document.getElementsByClassName("fabutime")[0].innerHTML= fabutime;
    </script> -->

    <script>
        //存取localStorage中的数据
        var store = {
            save(key,value){
                window.localStorage.setItem(key,JSON.stringify(value));
            },
            fetch(key){
                return JSON.parse(window.localStorage.getItem(key))||[];
            }
        }
        //list取出所有的值
        var list = store.fetch("storeData");

        var vm = new Vue({
            el:".main",
            data:{
                list,
                todo:'',
                edtorTodos:'',//记录正在编辑的数据,
                beforeTitle:"",//记录正在编辑的数据的title
                visibility:"all"//通过这个属性值的变化对数据进行筛选
            },
            watch:{
                //下面的这种方法是浅监控
                /*list:function(){//监控list这个属性，当这个属性对应的值发生变化就会执行函数
                    store.save("storeData",this.list);
                }*/

                //下面的是深度监控
                list:{
                    handler:function(){
                        store.save("storeData",this.list);
                    },
                    deep:true
                }

            },

            methods:{
                enterFn(ev){//添加任务
                    //向list中添加一项任务
                    //事件处理函数中的this指向的是当前这个根实例
                    if(this.todo==""){return;}
                    this.list.push({
                        title:this.todo,
                        isComplete:false
                    });
                    this.todo = "";

                },
                delFn(item){//删除任务
                    var index = this.list.indexOf(item);
                    this.list.splice(index,1)
                },
                edtorTodo(item){//编辑任务
                    //编辑任务的时候记录编辑之前的值
                    this.beforeTitle = item.title;
                    this.edtorTodos = item;
                },
                edtoEnd(item){//编辑完成
                    this.edtorTodos="";
                    // this.cancelEdit = this.edtorTodos;
                },
                cancelEdit(item){//取消编辑
                    item.title = this.beforeTitle;
                    this.beforeTitle = '';
                    this.edtorTodos='';
                }
            },
            directives:{
                "focus":{
                    update(el,binding){
                        if(binding.value){
                            el.focus();
                        }
                    }
                }
            },
            computed:{
                unComplete(){
                    return  this.list.filter(item=>{
                        return !item.isComplete
                    }).length
                },
                filterData(){
                    //过滤的时候有三种情况 all completed unCompleted
                    var filter = {
                        all:function(list){
                            return list;
                        },
                        completed:function(list){
                            return list.filter(item=>{
                                return item.isComplete;
                            })
                        },
                        unCompleted:function(list){
                            return list.filter(item=>{
                                return !item.isComplete;
                            })
                        }
                    }
                    //如果找到了过滤函数，就返回过滤后的数据，如果没有找到就返回所有的数据
                    return filter[this.visibility]?filter[this.visibility](list):list;
                }

            }
        });
        function hashFn(){
            var hash = window.location.hash.slice(1);
            vm.visibility = hash;
        }
        hashFn();
        window.addEventListener('hashchange',hashFn);
    </script>
</div>

</div>


<!--人生清单创意结束-->
````

文章排序和使用thymeleaf模板引擎渲染

````html
<h1>msos博客论坛文章</h1>

<!--普通排序文章-->
<article id="articles" class="container articles" style="padding-top: 2.5px">
    <div class="row article-row">
        <div class="article col s12 m6 l4" data-aos="zoom-in" th:each="article : ${article}">
            <div class="card z-depth-5">
                <style>
                    .card-image:hover .title-V{
                        display: none;
                    }
                    article .card-image-V:before, article .card-image-V:after{
                        top: -10.5%;

                    }
                </style>
                <a th:href="'/read?article_title='+${article.article_title}">

                    <div class="card-image card-image-V">
                        <img class="responsive-img lazyload" href="/article/read/V_hsV0o60j" src="https://codecheng-1305009997.cos.ap-chengdu.myqcloud.com/img/20210607223152.jpg"  />
                        <span class="card-title title-V" th:text="${article.article_title}"></span>
                        <div class="box-content">
                            <h3 class="title">阅读全文</h3>
                            <span class="post" style="width: 200px;color: black;"></span>
                        </div>
                    </div> </a>
                <div class="card-content article-content">
                    <div class="summary block-with-text" th:text="${article.article_content}">

                    </div>
                    <div class="publish-info">
                        <span class="publish-date" th:text="${article.article_time}"> <i class="far fa-calendar-minus"></i>  </span>
                        <span class="publish-author"> <i class="fa fa-bookmark fa-fw icon-category"></i> <a th:text="${article.article_type}" class="post-category"> </a> </span>
                    </div>
                </div>
                <div class="card-action article-tags">
                    <a th:href="'/read?article_title='+${article.article_title}" th:text="${article.article_title}"> <span class="chip bg-color" style="transition: all .4s;"></span> </a>
                </div>
            <!--        -->
                <div class="f-fr" style="position:relative;left: 250px;bottom: 25px;">
									<span class="read">
										<i class="fa fa-eye fs-16"></i>
										<i class="num" th:text="${article.article_views}"></i>
									</span>&nbsp;&nbsp;
                    <span class="ml20">
										<i class="fa fa-comments fs-16"></i>
										<a href="javascript:void(0)" class="num fc-grey" th:text="${article.article_comment_count}"></a>
									</span>
                </div>
            </div>
        </div>

</article>
            <!--文章置顶内容结束-->
````

搜索功能展示

```html
<!-- 搜索遮罩框开始 -->
<div id="searchModal" class="modal">
    <div class="modal-content">
        <div class="search-header">
            <span class="title"><i class="fa fa-search"></i>&nbsp;&nbsp;搜索</span>
            <form action="/selectArticle" method="get">
                <input type="text" id="article_title" name="article_title" placeholder="请输入搜索的关键字" class="search-input" />
                <button class="waves-effect waves-light btn" style="display: inline;" type="submit"> <i class="fa fa-search"></i> </button>
            </form>
        </div>
        <div id="searchResult"></div>
    </div>
</div>
<!-- 搜索遮罩框结束 -->
```

页脚设计和版权声明

```html
<footer class="footer wow fadeInUp" id="contact">
    <div class="footer-top">
        <div class="container">
            <div class="layui-row">
                <div class="layui-col-xs12 layui-col-sm6 layui-col-md4">
                    <div class="single-widget about">
                        <div class="footer-logo">
                            <h2 style="font-family: 楷体">进击的攻城狮</h2>
                        </div>
                        <p style="font-family: 楷体">扬帆起航,眼里有星辰大海。</p>
                        <div class="button">
                            <a href="/aboutMe" style="font-family: 楷体" class="btn layui-btn layui-btn-normal">关于进击的攻城狮</a>
                        </div>
                    </div>
                </div>
                <div class="layui-col-xs12 layui-col-sm6 layui-col-md4">
                    <div class="single-widget">
                        <h2 style="font-family: 楷体">相关链接</h2>
                        <ul class="social-icon">
                            <li class="active"><a href="/article"><i class="fa fa-book"></i>msos文章</a></li>
                            <li class="active"><a href="/message"><i class="fa fa-comments"></i>msos留言板</a></li>
                            <li class="active"><a href="javascript:void(0)"  onclick="qqShare('http://60.205.188.140:8888/','心如止水,明镜致远','msos',null,'http://60.205.188.140:8888/image/501664112.jpg')"><i class="fa fa-share"></i>分享</a></li>
                            <li class="active"><a href="/aboutMe"><i class="fa fa-snowflake-o"></i>关于msos</a></li>
                            <li class="active"><a href="/link"><i class="fa fa-files-o"></i>msos友链</a></li>
                        </ul>
                    </div>
                </div>
                <div class="layui-col-xs12 layui-col-sm12 layui-col-md4">
                    <div class="single-widget contact">
                        <h2 style="font-family: 楷体">进击的攻城狮</h2>
                        <ul class="list">
                            <li><i class="fa fa-map"></i>地址: 贵阳观山湖区云潭南路609号</li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <div class="copyright">
        <div class="container">
            <div class="layui-row">
                <div class="layui-col-xs12 layui-col-sm12 layui-col-md12 text-center">
                    <p class="mt05">
                        <!--调整版权信息-->
                        Copyright &copy; 2021-2021  进击的攻城狮
                        <a style="margin-inline:5px" target="_blank" href="https://www.msos.club"><img src="https://img.shields.io/badge/Auth-%E8%BF%9B%E5%87%BB%E7%9A%84%E6%94%BB%E5%9F%8E%E7%8B%AE-%230f73ae" title="很高兴遇到你"></a>
                        &nbsp;&nbsp;<a style="color: white" href="https://www.msos.club/">&nbsp;msos.club</a> &nbsp;版权所有&nbsp;&nbsp<a style="margin-inline:5px" target="_blank" href="https://creativecommons.org/licenses/cc-by/4.0"><img src="https://img.shields.io/badge/Copyright-CC--BY%204.0-ee5b32?style=flat&logo=Chef" title="msos博客论坛采用cc-by 4.0国际许可协议进行许可"></a> ICP证:<a style="color: white" href="https://beian.miit.gov.cn/">&nbsp;黔ICP备2021001761号-4</a>
                    </p>
                </div>
            </div>
        </div>
    </div>
</footer>

<script src="../js/wow.min.js"></script>
<script src="../js/index.js"></script>
<!--页脚修改结束-->

```

按钮使用svg画出来，实现昼夜切换，直达留言板，评论区功能

````
<!--按钮修改开始-->
<div class="menu-V">
    <div class="container-M">
        <div class="toggle"></div>
    </div>
    <svg aria-hidden="true" style="position: absolute;overflow: hidden;width: 0;height: 0">
        <symbol id="icon-sun" viewBox="0 0 1024 1024">
            <path d="M960 512l-128 128v192h-192l-128 128-128-128H192v-192l-128-128 128-128V192h192l128-128 128 128h192v192z" fill="#FFD878" p-id="8420"></path><path d="M736 512a224 224 0 1 0-448 0 224 224 0 1 0 448 0z" fill="#FFE4A9" p-id="8421"></path><path d="M512 109.248L626.752 224H800v173.248L914.752 512 800 626.752V800h-173.248L512 914.752 397.248 800H224v-173.248L109.248 512 224 397.248V224h173.248L512 109.248M512 64l-128 128H192v192l-128 128 128 128v192h192l128 128 128-128h192v-192l128-128-128-128V192h-192l-128-128z" fill="#4D5152" p-id="8422"></path><path d="M512 320c105.888 0 192 86.112 192 192s-86.112 192-192 192-192-86.112-192-192 86.112-192 192-192m0-32a224 224 0 1 0 0 448 224 224 0 0 0 0-448z" fill="#4D5152" p-id="8423"></path>
        </symbol>
        <symbol id="icon-moon" viewBox="0 0 1024 1024">
            <path d="M611.370667 167.082667a445.013333 445.013333 0 0 1-38.4 161.834666 477.824 477.824 0 0 1-244.736 244.394667 445.141333 445.141333 0 0 1-161.109334 38.058667 85.077333 85.077333 0 0 0-65.066666 135.722666A462.08 462.08 0 1 0 747.093333 102.058667a85.077333 85.077333 0 0 0-135.722666 65.024z" fill="#FFB531" p-id="11345"></path><path d="M329.728 274.133333l35.157333-35.157333a21.333333 21.333333 0 1 0-30.165333-30.165333l-35.157333 35.157333-35.114667-35.157333a21.333333 21.333333 0 0 0-30.165333 30.165333l35.114666 35.157333-35.114666 35.157334a21.333333 21.333333 0 1 0 30.165333 30.165333l35.114667-35.157333 35.157333 35.157333a21.333333 21.333333 0 1 0 30.165333-30.165333z" fill="#030835" p-id="11346"></path>
        </symbol>
    </svg>
    <a onclick="switchNightMode()" class="icon-V hidden" title="切换主题">
        <svg width="35" height="35" viewBox="0 0 1024 1024"><use id="modeicon" xlink:href=""></use></svg>
    </a>
    <a href="/message" class="icon-V hidden" title="前往留言板">
        <svg t="1612414295685" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="82057" width="35" height="35"><path d="M114.0736 546.304l751.1552-371.712-529.0496 444.7232zM951.7568 159.8976L556.0832 678.4l348.8768 58.9312 21.9648-14.592z" fill="#FBC07C" p-id="82058"></path><path d="M874.9056 216.9344l-477.6448 423.5264 99.7888 212.1728 8.6528-186.9312z" fill="#FC9553" p-id="82059"></path><path d="M542.72 888.3712v-185.0368l10.9056-15.104 115.712 17.2544z" fill="#E56234" p-id="82060"></path><path d="M962.4064 96.3072c-1.8432-1.8432-4.0448-3.072-6.3488-3.84-4.0448-1.6896-8.704-1.7408-12.9536 0.2048-7.2192 3.3792-722.5856 339.6096-874.9568 410.368a27.23328 27.23328 0 0 0-15.7696 26.6752 27.09504 27.09504 0 0 0 19.2512 24.2688l253.9008 78.1312 164.4032 312.7296a16.44032 16.44032 0 0 0 14.592 8.8064c0.1024 0 0.2048-0.0512 0.3072-0.0512 0.8192 0.1024 1.6384 0.2048 2.4576 0.2048 5.4272 0 10.6496-2.6112 13.8752-7.2704l148.7872-214.8864c5.888-7.3728 10.2912-13.056 13.5168-17.5104l217.7536 38.0928c3.072 0.9728 6.2976 1.4336 9.472 1.4336 6.1952 0 12.3392-1.792 17.5616-5.3248a31.6928 31.6928 0 0 0 14.0288-25.088l24.7808-611.9424c0.0512-0.768-0.0512-1.536-0.1024-2.2528 0.4608-4.5056-1.024-9.2672-4.5568-12.7488zM852.48 169.216L332.6976 602.2144l-243.712-74.9568C217.1392 467.6096 651.4688 263.6288 852.48 169.216z m-496.9472 453.9904l481.8432-401.408-320.0512 404.7872-24.6272 30.8224-2.3552 4.7104v217.4976l-134.8096-256.4096z m289.8432 89.9584l-124.3648 179.5584v-206.8992l128 22.3744c-1.792 2.4576-3.1744 4.352-3.6352 4.9664z m266.1888 8.96v0.0512c0 0.1536 0 0.4608-0.4096 0.7168-0.3584 0.256-0.6656 0.1536-0.8192 0.1024l-1.3312-0.512-229.5296-40.1408-146.4832-26.0608 7.6288-9.6256L934.5536 153.6l-22.9888 568.5248z" fill="#333333" p-id="82061"></path></svg>

    </a>
    <a href="#comment" class="icon-V hidden" id="toComment" title="前往评论区">
        <svg t="1612414443145" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="1879" width="38" height="38"><path d="M113.834667 291.84v449.194667a29.013333 29.013333 0 0 0 28.842666 29.013333h252.928v90.453333l160.597334-90.453333h252.928a29.013333 29.013333 0 0 0 29.013333-29.013333V291.84a29.013333 29.013333 0 0 0-29.013333-29.013333h-665.6a29.013333 29.013333 0 0 0-29.696 29.013333z" fill="#FFDEAD" p-id="1880"></path><path d="M809.130667 262.826667h-665.6a29.013333 29.013333 0 0 0-28.842667 29.013333v40.106667a29.013333 29.013333 0 0 1 28.842667-29.013334h665.6a29.013333 29.013333 0 0 1 29.013333 29.013334V291.84a29.013333 29.013333 0 0 0-29.013333-29.013333z" fill="#FFF3DB" p-id="1881"></path><path d="M556.202667 770.048h252.928a29.013333 29.013333 0 0 0 29.013333-29.013333V362.837333s-59.733333 392.533333-724.309333 314.709334v63.488a29.013333 29.013333 0 0 0 28.842666 29.013333h253.098667v90.453333z" fill="#F2C182" p-id="1882"></path><path d="M619.008 632.32l101.888-35.157333-131.754667-76.117334 29.866667 111.274667zM891.904 148.992a61.44 61.44 0 0 0-84.138667 22.528l-19.968 34.133333 106.666667 61.610667 19.968-34.133333a61.781333 61.781333 0 0 0-22.528-84.138667z" fill="#69BAF9" p-id="1883"></path><path d="M775.338667 198.775467l131.669333 76.032-186.026667 322.218666-131.6864-76.032z" fill="#F7FBFF" p-id="1884"></path><path d="M775.168 198.826667l-5.290667 9.216 59.221334 34.133333a34.133333 34.133333 0 0 1 12.458666 46.592l-139.946666 242.346667a34.133333 34.133333 0 0 1-46.762667 12.629333l-59.050667-34.133333-6.656 11.434666 88.746667 51.2L720.896 597.333333l186.026667-322.56z" fill="#D8E3F0" p-id="1885"></path><path d="M616.448 622.592l2.56 9.728 101.888-35.157333-44.885333-25.941334-59.562667 51.370667zM891.904 148.992c-1.024 0-2.218667-0.853333-3.242667-1.536A61.610667 61.610667 0 0 1 887.466667 204.8l-19.968 34.133333-73.728-42.496-5.12 8.704 106.666666 61.610667 19.968-34.133333a61.781333 61.781333 0 0 0-23.381333-83.626667z" fill="#599ED4" p-id="1886"></path><path d="M265.898667 417.621333H494.933333a17.066667 17.066667 0 1 0 0-34.133333H265.898667a17.066667 17.066667 0 1 0 0 34.133333zM265.898667 533.504H494.933333a17.066667 17.066667 0 0 0 0-34.133333H265.898667a17.066667 17.066667 0 0 0 0 34.133333z" fill="#3D3D63" p-id="1887"></path><path d="M959.488 354.645333a99.84 99.84 0 0 0-23.722667-127.488 78.677333 78.677333 0 0 0-142.848-64.170666l-11.605333 20.138666a17.066667 17.066667 0 0 0-20.821333 7.168l-32.085334 55.466667H142.677333a46.250667 46.250667 0 0 0-45.909333 46.08v449.194667a46.08 46.08 0 0 0 45.909333 46.08h236.032v73.386666a17.066667 17.066667 0 0 0 8.362667 14.848 17.066667 17.066667 0 0 0 8.704 2.218667 17.066667 17.066667 0 0 0 8.362667-2.218667l156.672-88.234666h248.32a46.08 46.08 0 0 0 46.08-46.08V398.677333L921.6 283.306667a17.066667 17.066667 0 0 0-4.266667-21.504l1.877334-3.413334a65.365333 65.365333 0 0 1 10.410666 79.189334l-53.077333 91.989333a56.832 56.832 0 0 0 20.821333 77.653333 17.066667 17.066667 0 0 0 24.234667-6.314666 17.066667 17.066667 0 0 0-6.997333-23.04 23.04 23.04 0 0 1-8.362667-31.061334z m-138.410667 386.389334a11.946667 11.946667 0 0 1-11.946666 11.946666H556.202667a17.066667 17.066667 0 0 0-8.362667 2.218667l-134.997333 76.117333v-61.269333a17.066667 17.066667 0 0 0-17.066667-17.066667H142.677333a11.946667 11.946667 0 0 1-11.776-11.946666V291.84a11.946667 11.946667 0 0 1 11.776-11.946667h565.930667L574.464 512a17.066667 17.066667 0 0 0-1.706667 12.970667L597.333333 615.253333H265.898667a17.066667 17.066667 0 1 0 0 34.133334h352.938666a17.066667 17.066667 0 0 0 5.802667 0l102.4-35.328a17.066667 17.066667 0 0 0 9.216-7.509334l85.333333-147.968z m-204.8-184.661334l63.829334 36.864-49.322667 17.066667z m206.848-170.666666v1.365333l-108.373333 186.709333-102.4-59.050666L781.482667 221.866667l102.4 59.050666z m76.458667-161.28L887.466667 244.224l-76.970667-44.373333 11.264-19.797334a44.544 44.544 0 1 1 77.141333 44.544z" fill="#3D3D63" p-id="1888"></path></svg>
    </a>
</div>

<!--返回顶部按钮开始-->
<div id="backTop" class="top-scroll">
    <a class="btn-floating btn-large waves-effect waves-light" title="返回顶部" href="#!">
        <svg t="1612414348421" style="position: relative;top: 5px" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="82219" width="38" height="38"><path d="M404.0704 372.224V231.936s-0.0512-94.5152 133.8368-155.2896c40.3968 17.7664 94.464 68.864 105.0624 154.0608v108.4928l-32.8192 49.664s-57.3952-94.7712-100.608-116.8384c-25.088 22.6816-73.5744 94.2592-79.9744 121.7536-16.896 17.664-19.1488-15.0016-25.4976-21.5552z" fill="#E56A77" p-id="82220"></path><path d="M154.368 824.9856v20.0192c0 18.2272 14.7968 33.024 33.024 33.024h225.28v-273.7664l-245.76 194.816a33.21344 33.21344 0 0 0-12.544 25.9072z" fill="#BC9BE0" p-id="82221"></path><path d="M322.56 296.192S226.304 349.1328 226.304 452.6592v264.9088l192.512-162.2528V452.6592C418.7648 335.872 322.56 296.192 322.56 296.192zM736.6144 301.312s93.6448 52.9408 93.6448 156.4672v264.9088l-187.2384-162.2528V457.7792c-0.0512-116.7872 93.5936-156.4672 93.5936-156.4672z" fill="#FFA750" p-id="82222"></path><path d="M642.9696 591.2064v286.8736h238.336c18.944 0 34.3552-15.36 34.3552-34.3552v-20.736c0-10.496-4.8128-20.4288-13.056-26.9312l-259.6352-204.8512zM606.3616 503.9616c0-146.3808-75.8272-200.3456-75.8272-200.3456S446.2592 360.448 446.2592 503.9616v374.0672h160.1536c-0.0512 0.0512-0.0512-227.6864-0.0512-374.0672z" fill="#BC9BE0" p-id="82223"></path><path d="M348.1088 971.6224h-44.4416c-11.6224 0-21.7088-7.7312-24.2688-18.6368l-11.6224-49.3056h119.0912l-14.8992 50.5344c-2.9696 10.2912-12.7488 17.408-23.8592 17.408zM762.8288 971.6224h-44.4416c-11.6224 0-21.7088-7.7312-24.2688-18.6368l-11.6224-49.3056h119.0912l-14.8992 50.5344c-2.9696 10.2912-12.7488 17.408-23.8592 17.408z" fill="#FFA750" p-id="82224"></path><path d="M910.336 772.9664l-64.768-51.0976V443.1872c0-136.6528-120.5248-184.9856-121.7536-185.4464-4.096-1.5872-8.704-1.3312-12.5952 0.6656-1.8432 0.9728-19.6608 10.3936-41.0624 28.3648v-40.7552c0-150.016-152.064-202.5472-153.6-203.0592a15.1552 15.1552 0 0 0-11.1104 0.5632c-6.1952 2.7648-152.2176 69.376-152.2176 202.496V286.72c-24.832-20.1216-46.4384-28.7744-46.9504-28.9792-4.096-1.5872-8.704-1.3312-12.5952 0.6656-4.9152 2.56-120.2176 63.5904-120.2176 184.7296v282.3168l-59.904 47.5136a54.016 54.016 0 0 0-20.5824 42.5472v23.6032c0 29.952 24.3712 54.3232 54.3232 54.3232h69.4784l12.6976 55.9104c5.0176 22.1696 24.4224 37.632 47.1552 37.632h58.88c21.504 0 40.6528-14.4384 46.4896-35.1232l16.5888-58.4192h229.1712l16.5888 58.4192c5.888 20.6848 24.9856 35.1232 46.4896 35.1232h58.88c22.7328 0 42.1376-15.4624 47.1552-37.632l12.6976-55.9104h67.1744c29.952 0 54.3232-24.3712 54.3232-54.3232v-23.5008c-0.0512-16.7424-7.5776-32.3072-20.736-42.6496z m-270.848-455.7824c-13.3632 15.6672-25.856 34.5088-34.8672 56.576-8.5504-24.2176-19.4048-44.0832-30.5664-60.0064h65.4336v3.4304z m-17.7664 187.8016h193.1264v35.072h-193.1264v-35.072z m32.4096 65.792h160.768v126.8224l-0.5632-0.4608-160.2048-126.3616z m65.024-281.4464c22.3744 11.1104 95.744 55.1424 95.744 153.856v31.1296h-193.1264v-31.1296c0-44.9024 19.8144-80.5888 42.0864-106.5984 1.792-1.28 3.2768-2.9696 4.352-4.9152 19.8656-21.8624 40.8064-36.1472 50.944-42.3424z m-206.592-215.1424c25.7024 10.24 126.9248 57.9072 126.9248 171.776v37.0176h-91.392c-16.5376-16.1792-29.696-23.6544-31.232-24.4736a15.42144 15.42144 0 0 0-16.384 1.0752c-1.3312 0.9728-11.776 8.7552-25.6 23.3984H383.9488v-37.0176c0-99.7888 103.4752-158.8736 128.6144-171.776z m-308.3776 496.5888h164.4032l-164.4032 130.3552v-130.3552z m0-65.792H397.312v35.072H204.1856v-35.072zM416.768 374.9888c-8.1408-23.04-19.9168-42.1888-32.768-57.856v-3.328h65.792a280.5248 280.5248 0 0 0-33.024 61.184zM301.6192 289.28c22.6816 11.0592 95.6928 54.4256 95.6928 153.9072v31.1296H204.1856v-31.1296c0-87.5008 75.1104-140.1856 97.4336-153.9072zM123.6992 839.1168v-23.6032c0-7.2704 3.2768-13.9776 8.9088-18.4832l264.704-209.8688v275.5072H147.2512c-13.0048 0.0512-23.552-10.5472-23.552-23.552z m228.7104 104.2944a17.71008 17.71008 0 0 1-16.9472 12.8h-58.88c-8.2944 0-15.36-5.632-17.2032-13.7216l-11.1616-49.1008H366.592l-14.1824 50.0224z m75.6224-387.9936V480.4608c0-105.1136 60.5184-169.3696 82.5856-189.2864 22.3744 16.4864 80.384 70.7584 80.384 189.2864v382.208h-63.9488V437.4528c0-8.4992-6.8608-15.36-15.36-15.36s-15.36 6.8608-15.36 15.36v425.2672H428.032v-307.3024z m338.8416 387.1232a17.54112 17.54112 0 0 1-17.2032 13.7216h-58.88c-7.8336 0-14.7968-5.2736-16.9472-12.8l-14.1824-50.0224h118.3744l-11.1616 49.1008z m133.4272-103.424c0 13.0048-10.5984 23.6032-23.6032 23.6032h-254.976v-278.3232l199.0144 157.0304 70.6048 55.7056c5.6832 4.5056 8.96 11.264 8.96 18.5344v23.4496z" fill="#333333" p-id="82225"></path></svg>
    </a>
</div>
<!--返回顶部按钮结束-->
<!--按钮修改结束-->
````

------

## 关于页面实现ABOUT

> 采用linux风格的介绍，色彩搭配，布局，介绍进击的攻城狮团队，msos博客论坛

````
 <!--关于内容修改开始-->
    <div id="box">
        <!-- 个人资料卡片 -->
        <div class="meBox">
            <!-- 头像 -->
            <div class="headPhoto"></div>
            <!-- 介绍 -->
            <div class="meBox-title">
                <p> MSOS </p>
                <div class="fg"></div>
            </div>
            <div class="meBox-text">
                <p>Blue风格的博客论坛  🎯</p>
                <p>🎈 💖</p>
                <p>进击的攻城狮 🐬</p>
                <p>要做最好看的博客论坛 💪</p>
                <p>热爱前端💻后端📷UI🚴数据库 </p>
            </div>
            <!-- 两个按钮 -->
            <div class="meBox-Button">
                <!--<a href="/homepage.html">msos博客论坛首页🤣</a><br>-->

            </div>
        </div>

        <!-- 伪终端介绍 -->
        <div id="cmdBox">
            <!-- 第一个终端 -->
            <div class="cmd">
                <!-- 三个按钮 -->
                <div class="click">
                    <div class="red"></div>
                    <div class="yellow"></div>
                    <div class="green"></div>
                </div>
                <!-- 顶部标题 -->
                <div class="title">
                    <span>msos - bash</span>
                </div>
                        <!-- 终端内文字 -->
                <div class="cmdText">

                    <span style="color: rgb(0, 190, 0);">root@msos</span>
                    <span style="color: blue;">~</span>
                    <span style="color: rgb(39, 39, 39);">cat ./msos.txt</span>
                    <p>昵称：msos</p>
                    <p>创始人：进击的攻城狮</p>
                    <p>时间：1个月</p>
                    <p>地址：贵州，贵阳</p>
                    <p>邮箱：msos-dyzz@gmail.com</p>
                    其他：做个好看的博客论坛，留存点温柔~
                    <br>

                    <p>主要方向博客,论坛</p>
                    <p>这条路才刚刚迈开了第一步</p>
                    <span style="color: rgb(0, 190, 0);">root@msos</span>
                    <span style="color: blue;">~</span>
                    <span style="color: rgb(39, 39, 39);">sudo rm -rf ./一切的Bug和错误/*</span>
                    <p>sudo: 请输入密码: *******</p>
                    <p>bash:  请再次确认是否删除，您准备好了吗？(y/n) </p>
                    <span style="color: rgb(0, 190, 0);">root@msos</span>
                    <span style="color: blue;">~ y<span id="Y"></span></span>
                </div>
            </div>
            <!-- 第二个终端 -->
            <div class="cmd cmd2">
                <!-- 三个按钮 -->
                <div class="click">
                    <div class="red"></div>
                    <div class="yellow"></div>
                    <div class="green"></div>
                </div>
                <!-- 顶部标题 -->
                <div class="title">
                    <span>msos- bash</span>
                </div>
                <!-- 终端内文字 -->
                <div class="cmdText">
                    <span style="color: rgb(0, 190, 0);">root@msos</span>
                    <span style="color: blue;">~</span>
                    <span style="color: rgb(39, 39, 39);">./links.sh</span>
                    <p>我的站点：</p>
                    <ul class="ul">
                        <li><a href="https://www.msos.club">Msos博客论坛</a></li>
                        <li><a href="https://github.com/">Github</a></li>
                        <li><a href="#">About</a></li>
                    </ul>
                    <span style="color: rgb(0, 190, 0);">root@msos</span>
                    <span style="color: blue;">~</span>
                    <span style="color: rgb(39, 39, 39);">./yiyan.sh</span>
                    <p class="hito">踏足其中,云开雾散.</p>
                    <span style="color: rgb(0, 190, 0);">root@msos</span>
                    <span style="color: blue;">~</span>
                    <span style="color: rgb(39, 39, 39);">./ip.sh</span>
                    <p class="getip"></p>
                    <span style="color: rgb(0, 190, 0);">root@msos</span>
                    <span style="color: blue;">~</span>
                    <span style="color: rgb(39, 39, 39);">./autoPlayer.sh</span>
                    <p>[autoPlayer]正在加载，请稍后...</p>
                    <div class="aplayer" data-id="31877628" data-server="netease" data-type="song" mini="true" data-volume="0.35"></div>
                </div>
            </div>
        </div>
    </div>

    <!-- 页脚内容 -->

    <script src="https://v1.hitokoto.cn/?encode=js&select=.hito" defer></script>
    <script src="https://pv.sohu.com/cityjson?ie=utf-8"></script>
    <script type="text/javascript">(function getip(selector){var ip="你的 IP: "+returnCitySN["cip"];var ele=document.querySelector(selector);Array.isArray(ele)?ele[0].innerText=ip:ele.innerText=ip;})('.getip')</script>
    <script src="https://cdn.jsdelivr.net/npm/aplayer@1.10.1/dist/APlayer.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/meting@1.1.0/dist/Meting.min.js"></script>	<!-- 360站长平台自动提交 -->
    <script>
        (function(){
            var src = "https://jspassport.ssl.qhimg.com/11.0.1.js?d182b3f28525f2db83acfaaf6e696dba";
            document.write('<script src="' + src + '" id="sozz"><\/script>');
        })();
    </script>
    <!--关于内容修改结束-->

````

### link友链界面实现

````html
<!--        友链主题内容开始-->
        <main class="content">
            <div class="container friends-container">
                <div class="card" style="top: -5rem">
                    <div class="card-content">
                        <div class="center-align">
                            <div class="V-title V-title-top">
                                <span><i class="fa fa-address-book"></i></span>
                                <span>&nbsp;&nbsp;友链添加</span>
                            </div>
                        </div>
                        <hr data-aos="fade-right">
                        <div style="height: 20px"></div>
                        <div class="mainV hide-on-med-and-down piano-message" data-aos="fade-left">
                            <div class="keyboard">
                                <div class="keyboard__front face-keyboard">
                                    <div class="keyboard__f-top">
                                        <div class="keyboard__speaker"></div>
                                        <div class="keyboard__buttons">
                                            <div class="keyboard__button"></div>
                                            <div class="keyboard__button"></div>
                                            <div class="keyboard__button"></div>
                                            <div class="keyboard__button"></div>
                                            <div class="keyboard__button"></div>
                                            <div class="keyboard__button"></div>
                                        </div>
                                        <div class="keyboard__led">
                                            <div class="keyboard__line">
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                            </div>
                                            <div class="keyboard__line">
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                            </div>
                                            <div class="keyboard__line">
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                            </div>
                                            <div class="keyboard__line">
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                            </div>
                                            <div class="keyboard__line">
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                            </div>
                                            <div class="keyboard__line">
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                            </div>
                                            <div class="keyboard__line">
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                            </div>
                                            <div class="keyboard__line">
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                            </div>
                                            <div class="keyboard__line">
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                            </div>
                                            <div class="keyboard__line">
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                                <div class="keyboard__dot"></div>
                                            </div>
                                        </div>
                                        <div class="keyboard__buttons">
                                            <div class="keyboard__button"></div>
                                            <div class="keyboard__button"></div>
                                            <div class="keyboard__button"></div>
                                            <div class="keyboard__button"></div>
                                            <div class="keyboard__button"></div>
                                            <div class="keyboard__button"></div>
                                        </div>
                                        <div class="keyboard__speaker"></div>
                                    </div>
                                    <div class="keyboard__f-bottom">
                                        <div class="key">
                                            <div class="key__front face-key key__front-1"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key">
                                            <div class="key__front face-key key__front-2"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key">
                                            <div class="key__front face-key key__front-3"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key">
                                            <div class="key__front face-key key__front-4"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key">
                                            <div class="key__front face-key key__front-5"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key">
                                            <div class="key__front face-key key__front-6"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key">
                                            <div class="key__front face-key key__front-7"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key">
                                            <div class="key__front face-key key__front-8"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key">
                                            <div class="key__front face-key key__front-9"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key">
                                            <div class="key__front face-key key__front-10"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key">
                                            <div class="key__front face-key key__front-11"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key">
                                            <div class="key__front face-key key__front-12"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key">
                                            <div class="key__front face-key key__front-13"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key">
                                            <div class="key__front face-key key__front-14"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key">
                                            <div class="key__front face-key key__front-15"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key">
                                            <div class="key__front face-key key__front-16"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key">
                                            <div class="key__front face-key key__front-17"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key">
                                            <div class="key__front face-key key__front-18"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key">
                                            <div class="key__front face-key key__front-19"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key">
                                            <div class="key__front face-key key__front-20"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key">
                                            <div class="key__front face-key key__front-21"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key key--black key--black-1">
                                            <div class="key__front face-key"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key key--black key--black-2">
                                            <div class="key__front face-key"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key key--black key--black-3">
                                            <div class="key__front face-key"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key key--black key--black-4">
                                            <div class="key__front face-key"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key key--black key--black-5">
                                            <div class="key__front face-key"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key key--black key--black-6">
                                            <div class="key__front face-key"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key key--black key--black-7">
                                            <div class="key__front face-key"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key key--black key--black-8">
                                            <div class="key__front face-key"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key key--black key--black-9">
                                            <div class="key__front face-key"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key key--black key--black-10">
                                            <div class="key__front face-key"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key key--black key--black-11">
                                            <div class="key__front face-key"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key key--black key--black-12">
                                            <div class="key__front face-key"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key key--black key--black-13">
                                            <div class="key__front face-key"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                        <div class="key key--black key--black-14">
                                            <div class="key__front face-key"></div>
                                            <div class="key__back face-key"></div>
                                            <div class="key__right face-key"></div>
                                            <div class="key__left face-key"></div>
                                            <div class="key__top face-key"></div>
                                            <div class="key__bottom face-key"></div>
                                        </div>
                                    </div>
                                </div>
                                <div class="keyboard__back face-keyboard"></div>
                                <div class="keyboard__right face-keyboard"></div>
                                <div class="keyboard__left face-keyboard"></div>
                                <div class="keyboard__top face-keyboard"></div>
                                <div class="keyboard__bottom face-keyboard"></div>
                            </div>
                        </div>
                        <div style="height: 30px"></div>
                        <div class="about-inner">
                            <div data-aos="fade-up">
                                <div class="card v-card">
                                    <div class="new-item-badge">
                                        留下你的信息
                                    </div>
                                    <div class="card-content v-order">
                                        <ol style="padding-inline-start: 5px !important;">
                                            <li><div style="font-size: 18px">这里是msos博客论坛的友链板，走过路过的朋友们可留下你的博客信息。</div> </li>
                                            <li><div style="font-size: 18px">交换友链前请先添加本站链接，通过留言，邮件告知
                                                你也可以通过此链接提交信息</div></li>
                                            <li><div style="font-size: 18px">  <br>- 可以在留言板，友链下方留下你的站点信息🎸
                                                - 你的站点信息：name💙 <br>
                                                - 你的站点网址：url🌛🌜 <br>
                                                - 你的图片头像：avatar⭐🌟 <br>
                                                - 你的站点描述：desc🌎🌏 <br></div></li>
                                        </ol>
                                    </div>
                                </div>
                            </div>
                            <!---->
                            <div style="height: 80px"></div>
                        </div>
                    </div>
                </div>
                <div data-aos="fade-up">
                    <div id="comment" class="card valine-card" style="top: -60px">
                        <img class="lazyload zoombe-comment" data-aos="slide-left" src="https://cdn.vino.run/img/Vino_2021-02-01-38-24-LodingPeer.jpeg" data-src="https://cdn.vino.run/img/Vino_2021-02-01-15-09-zoomb.gif" height="170px" width="170px" />
                        <div class="card-content">
                            <div class="comment_headling head-comment">
                                <i class="fa fa-comments" aria-hidden="true"></i>
                                <span>友链</span>
                                <div class="comment-switch">
                                    <span class="first-comment">Valine </span>
                                    <label class="switch"> <input type="checkbox" />
                                        <div class="sliderV round" id="sliderV"></div> </label>
                                    <span class="second-comment">  Gitalk</span>
                                </div>
                            </div>
                            <!-- Gitalk 评论 start  -->
                            <script src="https://cdn.bootcdn.net/ajax/libs/gitalk/1.7.0/gitalk.min.js"></script>
                            <div id="commentArea1" style="display:none;">
                                <div id="gitalk-container"></div>
                            </div>
                            <script type="text/javascript">
                                var gitalk = new Gitalk({
                                    // gitalk的主要参数
                                    clientID: `870291ffdff2235e0af4`,
                                    clientSecret: `f92e980c6b6996233d6f9b67d39d773244d6c012`,
                                    repo: `CommentData`,
                                    owner: 'Vino1016',
                                    admin: ['Vino1016'],
                                    id: 'FriendComments', //注意id一定不要重复，这里是举个例子，可以写中文，如果重复了，就会把其他地方的评论显示过来

                                });
                                gitalk.render('gitalk-container');
                            </script>
                            <!-- Gitalk end -->
                            <!--Valine-->
                            <div id="commentArea2">
                                <div style="height: 80px"></div>
                                <div id="vcomments"></div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </main>
<!--        友链主题内容结束-->
<!--友链板主题内容结束-->
````

### message留言板

````html
 <!--    留言板主题内容开始-->
        <div class="doc-container" id="doc-container">
            <div class="container-fixed">
                <div class="container-inner">
                    <section class="msg-remark">
                        <h1 style="font-family: 楷体">留言板</h1>
                        <p style="font-family: 楷体">
                            沟通交流，拉近你我！我们的<span style="color: red" th:text="${session.userCount}"></span>位小伙伴共同留下了<span style="color: red" th:text="${session.messageCount}"></span>条留言和回复哦!
                        </p>
                    </section>
                    <div class="textarea-wrap message" id="textarea-wrap">
                        <form class="layui-form" action="">
                            <div class="layui-form-item">
                                <textarea id="message_content" name="message_content" lay-verify="content" placeholder="请输入内容" class="layui-textarea"></textarea>
                            </div>
                            <div class="layui-form-item">
                                <button  id="submit" type="button" data-type="reload" class="layui-btn layui-btn-primary" >提交留言</button>
                            </div>
                        </form>
                    </div>
                </div>
                <div class="f-cb"></div>
                <div class="mt20">
                    <ul class="message-list" id="message-list">
                        <li class="zoomIn article" th:each="message0 : ${message}" th:if="not ${message0.message_parant_id}">
                            <div class="comment-parent">
                                <a name="remark-1"></a>
                                <img th:src="'http://blog-cxz.oss-cn-beijing.aliyuncs.com/'+${message0.user_id}+'.jpg'">
                                <div class="info">
                                    <span class="username" th:text="${message0.user_name}"></span>
                                </div>
                                <div class="comment-content" th:text="${message0.message_content}">
                                </div>
                                <p class="info info-footer">
                                    <i class="fa fa-map-marker" aria-hidden="true"></i>
                                    <span th:text="${message0.message_ip}"></span>
                                    <span class="comment-time" th:text="${message0.message_time}"></span>
                                    <a href="javascript:;" class="btn-reply" data-targetid="1" th:data-targetname="${message0.user_name}">回复</a>
                                </p>
                            </div>
                            <hr />

                            <div class="comment-child" th:each="message1 : ${message}" th:if="${message1.message_parant_id} eq ${message0.message_id}">
                                <a name="reply-1"></a>
                                <img th:src="'http://blog-cxz.oss-cn-beijing.aliyuncs.com/'+${message1.user_id}+'.jpg'">
                                <div class="info">
                                    <span class="username" th:text="${message1.user_name}"></span>
                                    <span th:text="${message1.message_content}"></span>
                                </div>
                                <p class="info">
                                    <i class="fa fa-map-marker" aria-hidden="true"></i>
                                    <span th:text="${message1.message_ip}"></span>
                                    <span class="comment-time" th:text="${message1.message_time}"></span>
                                </p>
                            </div>
                            <div class="replycontainer layui-hide">
                                <form class="layui-form" action="/childMessages" method="post">
                                    <input type="hidden" id="child_message_parant_id" name="child_message_parant_id" th:value="${message0.message_id}">
                                    <div class="layui-form-item">
                                        <textarea id="child_message_content" name="child_message_content" lay-verify="replyContent" placeholder="请输入回复内容" class="layui-textarea" style="min-height:80px;"></textarea>
                                    </div>
                                    <div class="layui-form-item">
                                        <button th:id="${message0.message_id}" type="submit" data-type="reload" class="layui-btn layui-btn-primary">提交</button>
                                    </div>
                                </form>
                            </div>
                            <hr>

                        </li>
                    </ul>
                </div>
            </div>
        </div>


</main>
<!--留言板主题内容结束-->
````

### login登录页面

````html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
	<head>
		<meta charset="utf-8">
		<title>登录msos</title>
		<!-- 样 式 文 件 -->
		<link rel="stylesheet" href="../component/pear/css/pear.css" />
<!--		<link rel="stylesheet" href="../css/xadmin.css">-->
		<link rel="stylesheet" href="../admin/css/other/login.css" />
		<link rel="shortcut icon" th:href="@{favicon.ico}" />
		<!--    修改样式引入开始-->
		<link rel="Bookmark" href="https://codecheng-1305009997.cos.ap-chengdu.myqcloud.com/img/20210604085540.png" type="image/x-icon" />
		<link rel="stylesheet" type="text/css" href="https://cdn.jsdelivr.net/gh/vino1016/cdn@2.44/static/matery/css/VinoAnimation.min.css" />
		<link rel="stylesheet" type="text/css" href="https://cdn.jsdelivr.net/gh/vino1016/cdn@2.40/static/css/blog.min.css" />
		<!--<link rel="stylesheet" type="text/css" href="https://cdn.jsdelivr.net/gh/vino1016/cdn@1.1/static/matery/css/materialize.min.css" />-->
		<link rel="stylesheet" type="text/css" href="https://cdn.jsdelivr.net/gh/vino1016/cdn@2.66/static/matery/css/matery.min.css" />
		<link rel="preload" as="style" href="https://cdn.bootcdn.net/ajax/libs/font-awesome/5.15.1/css/all.min.css" onload="this.onload=null;this.rel='stylesheet'"/>
		<link rel="stylesheet" type="text/css" href="https://cdn.bootcdn.net/ajax/libs/aos/3.0.0-beta.6/aos.css" />
		<link rel="preconnect" href="https://fonts.gstatic.com" />
		<!--倒计时模块-->
		<link href="https://fonts.googleapis.com/css2?family=Noto+Serif+SC&amp;family=Zhi+Mang+Xing&amp;family=Luckiest+Guy&amp;display=swap" rel="stylesheet" />
		<link rel="preconnect" href="https://fonts.gstatic.com">
		<link href="https://fonts.googleapis.com/css2?family=Noto+Serif+SC:wght@400;500;900&display=swap" rel="stylesheet" media="print" onload="this.media='all'">
		<!--    修改样式引入结束-->

		<style type="text/css" lang="css">
			#loading-container{
				position: fixed;
				top: 0;
				left: 0;
				min-height: 100vh;
				width: 100vw;
				z-index: 9999;
				display: flex;
				flex-direction: column;
				justify-content: center;
				align-items: center;
				background: #FFF;
				text-align: center;
				/* loader页面消失采用渐隐的方式*/
				-webkit-transition: opacity 1s ease;
				-moz-transition: opacity 1s ease;
				-o-transition: opacity 1s ease;
				transition: opacity 1s ease;
			}
			.loading-image{
				width: 120px;
				height: 50px;
				transform: translate(-50%);
			}

			.loading-image div:nth-child(2) {
				-webkit-animation: pacman-balls 1s linear 0s infinite;
				animation: pacman-balls 1s linear 0s infinite
			}

			.loading-image div:nth-child(3) {
				-webkit-animation: pacman-balls 1s linear .33s infinite;
				animation: pacman-balls 1s linear .33s infinite
			}

			.loading-image div:nth-child(4) {
				-webkit-animation: pacman-balls 1s linear .66s infinite;
				animation: pacman-balls 1s linear .66s infinite
			}

			.loading-image div:nth-child(5) {
				-webkit-animation: pacman-balls 1s linear .99s infinite;
				animation: pacman-balls 1s linear .99s infinite
			}

			.loading-image div:first-of-type {
				width: 0;
				height: 0;
				border: 25px solid #49b1f5;
				border-right-color: transparent;
				border-radius: 25px;
				-webkit-animation: rotate_pacman_half_up .5s 0s infinite;
				animation: rotate_pacman_half_up .5s 0s infinite;
			}
			.loading-image div:nth-child(2) {
				width: 0;
				height: 0;
				border: 25px solid #49b1f5;
				border-right-color: transparent;
				border-radius: 25px;
				-webkit-animation: rotate_pacman_half_down .5s 0s infinite;
				animation: rotate_pacman_half_down .5s 0s infinite;
				margin-top: -50px;
			}
			@-webkit-keyframes rotate_pacman_half_up {0% {transform: rotate(270deg)}50% {transform: rotate(1turn)}to {transform: rotate(270deg)}}

			@keyframes rotate_pacman_half_up {0% {transform: rotate(270deg)}50% {transform: rotate(1turn)}to {transform: rotate(270deg)}}

			@-webkit-keyframes rotate_pacman_half_down {0% {transform: rotate(90deg)}50% {transform: rotate(0deg)}to {transform: rotate(90deg)}}

			@keyframes rotate_pacman_half_down {0% {transform: rotate(90deg)}50% {transform: rotate(0deg)}to {transform: rotate(90deg)}}

			@-webkit-keyframes pacman-balls {75% {opacity: .7}to {transform: translate(-100px, -6.25px)}}

			@keyframes pacman-balls {75% {opacity: .7}to {transform: translate(-100px, -6.25px)}}


			.loading-image div:nth-child(3),
			.loading-image div:nth-child(4),
			.loading-image div:nth-child(5),
			.loading-image div:nth-child(6){
				background-color: #49b1f5;
				width: 15px;
				height: 15px;
				border-radius: 100%;
				margin: 2px;
				width: 10px;
				height: 10px;
				position: absolute;
				transform: translateY(-6.25px);
				top: 25px;
				left: 100px;
			}
			.loading-text{
				margin-bottom: 20vh;
				text-align: center;
				color: #2c3e50;
				font-size: 2rem;
				box-sizing: border-box;
				padding: 0 10px;
				text-shadow: 0 2px 10px rgba(0,0,0,0.2);
			}
			@media only screen and (max-width: 500px) {
				.loading-text{
					font-size: 1.5rem;
				}
			}
			.fadeout {
				opacity: 0;
				filter: alpha(opacity=0);
			}
			/* logo出现动画 */
			@-webkit-keyframes fadeInDown{0%{opacity:0;-webkit-transform:translate3d(0,-100%,0);transform:translate3d(0,-100%,0)}100%{opacity:1;-webkit-transform:none;transform:none}}
			@keyframes fadeInDown{0%{opacity:0;-webkit-transform:translate3d(0,-100%,0);}}
		</style>
		<script>
			(function () {
				const loaded = function(){
					setTimeout(function(){
						const loader = document.getElementById("loading-container");
						loader.className="fadeout" ;//使用渐隐的方法淡出loading page
						// document.getElementById("body-wrap").style.display="flex";
						setTimeout(function(){
							loader.style.display="none";
						},1000);
					},1000);//强制显示loading page 1s
				};
				loaded();
			})()
		</script><meta name="generator" content="Hexo 5.4.0">
		<style>
			<!--背景像素纹理美化-->
			body::before {
				background-image: url(https://cdn.jsdelivr.net/gh/moezx/cdn@3.1.9/img/Sakura/images/grid.png);
			}
			.github-emoji { position: relative; display: inline-block; width: 1.2em; min-height: 1.2em; overflow: hidden; vertical-align: top; color: transparent; }  .github-emoji > span { position: relative; z-index: 10; }  .github-emoji img, .github-emoji .fancybox { margin: 0 !important; padding: 0 !important; border: none !important; outline: none !important; text-decoration: none !important; user-select: none !important; cursor: auto !important; }  .github-emoji img { height: 1.2em !important; width: 1.2em !important; position: absolute !important; left: 50% !important; top: 50% !important; transform: translate(-50%, -50%) !important; user-select: none !important; cursor: auto !important; } .github-emoji-fallback { color: inherit; } .github-emoji-fallback img { opacity: 0 !important; }</style>
		<link rel="alternate" href="/atom.xml" title="CodeCheng" type="application/atom+xml">
		<!--加载动画样式结束-->
	</head>
    <!-- 代 码 结 构 -->
	<body background="../admin/images/background.svg" style="background-size: cover;">
	<!--加载动画开始-->
	<div id="loading-container">
		<p class="loading-text">慢慢来，是种诚意，msos论坛加载中 . . . </p>
		<div class="loading-image">
			<div></div>
			<div></div>
			<div></div>
			<div></div>
			<div></div>
		</div>
	</div>
	<!--加载动画结束-->


		<form class="layui-form" action="javascript:void(0);">
			<div class="layui-form-item">
				<img class="logo" src="https://codecheng-1305009997.cos.ap-chengdu.myqcloud.com/img/20210603234521.png" />
				<div class="title" style="font-family: 楷体">msos 博客论坛</div>
				<div class="desc" style="font-family: 楷体">
					欢迎登陆msos--进击的攻城狮
				</div>
			</div>
			<div class="layui-form-item">
				<input id="user_id"name="user_id" placeholder="请输入账号 :" lay-verify="required" hover class="layui-input"  />
			</div>
			<div class="layui-form-item">
				<input id="user_password"name="user_password" type="password" placeholder="请输入密码 :" lay-verify="required" hover class="layui-input"  />
			</div>
			<div class="layui-form-item">
				<input id="yzm" placeholder="验证码 : "  hover  lay-verify="required" class="code layui-input layui-input-inline"  />
				<img src="../admin/images/captcha.gif" class="codeImage" />
			</div>
			<div class="layui-form-item">
				<input  type="checkbox" name="" title="记住密码" lay-skin="primary" checked>
				<a  id="butt2" type="button"  style="width:100%;" onclick="xadmin.open('忘记密码','/html/forgetPassword.html',500,250)">忘记密码</a>
			</div>
			<hr>
			<a id="butt" type="button"  style="width:100%;" onclick="xadmin.open('注册','/html/insertUser.html',500,500)">没有账号?点击注册</a>
			<div class="layui-form-item">
				<button id="btn" type="button" class="pear-btn pear-btn-success login" lay-submit lay-filter="login" >
					登录msos
				</button>
			</div>
		</form>



		<!-- 资 源 引 入 -->
		<script src="../component/js/jquery-3.3.1.js"></script>
		<script src="../component/layui/layui.js"></script>
		<script src="../component/pear/pear.js"></script>
		<script type="text/javascript" src="../component/js/xadmin.js"></script>
		<script language="javascript">
			var input =document.getElementById("yzm")

			input.addEventListener("keyup",function (event)
			{
				event.preventDefault();
				if(event.keyCode === 13){
					document.getElementById("btn").click();
				}
			})
		</script>
		<script>
			layui.use(['form', 'button', 'popup'], function() {
				var form = layui.form;
				var button = layui.button;
				var popup = layui.popup;

                // 登 录 提 交
				form.on('submit(login)', function() {
					/// 验证
					$.ajax(
							{
								type: "post",
								url:"/user/toLogin",
								data: {"user_id":$("#user_id").val(),"user_password":$("#user_password").val()},
								dataType: "json",
								success:function (data) {
									if(data.token!=null){
										button.load({
											elem: '.login',
											time: 1000,
											done: function() {
												console.log(data)
												popup.success("登录成功!", function() {
								window.location.href = "/login?token="+data.token+"&user_id="+data.user_id+"&user_role="+data.user_role
					                    });
					                        }
										})
									}else {
										button.load({
											elem: '.login',
											time: 1000,
											done: function() {
												popup.success("账号/密码错误!", function() {

												});
											}
										})
									}
								},
								error:function () {
									button.load({
										elem: '.login',
										time: 1500,
										done: function() {
											popup.success("登录出错啦!", function() {
											});
										}
									})
								}
							}
					)
					/// 登录
					return false;
				
				});
			})


			/**
			 * 判断用户名和密码的正则表达式
			 */
			$("#user_id").blur(function () {
				var userName = /^[A-Z][A-Za-z0-9]_${6,20}/;
				way("name",userName);

				var nameStr = $("#nameReg").text();
				if(nameStr == "×"){
					$("#user_id").css("border-color","red");
				}else{
					$("#user_id").css("border","");
				}
			});
			$("#user_password").blur(function () {
				//
				var password = /^[A-Z][a-z0-9_]{8,15}$/;
				way("user_password",password);

				var pwdStr = $("#pwdReg").text();
				if(pwdStr == "×"){
					$("#user_password").css("border-color","red");
				}else{
					$("#user_password").css("border","");
				}
			});

		</script>
	<!--鼠标跟随彩虹-->
	<script src="https://cdn.jsdelivr.net/gh/Yafine/cdn@2.5/source/js/cursor.js"></script>
	<!--点击文字效果-->
	<script>
		var a_idx = 0;
		jQuery(document).ready(function ($) {
			$("body").click(function (e) {
				var a = new Array("msos欢迎你", "快来就加入我们", "dyzz", "快来登录", "点击注册吧", "进击的攻城狮" );
				var $i = $("<span/>").text(a[a_idx]);
				a_idx = (a_idx + 1) % a.length;
				var x = e.pageX,
						y = e.pageY;
				$i.css({
					"z-index": 5,
					"top": y - 20,
					"left": x,
					"position": "absolute",
					"font-weight": "bold",
					"color": "#5056ce"
				});
				$("body").append($i);
				$i.animate({
							"top": y - 180,
							"opacity": 0
						},
						3000,
						function () {
							$i.remove();
						});
			});
			setTimeout('delay()', 2000);
		});

		function delay() {
			$(".buryit").removeAttr("onclick");
		}

	</script>
	</body>
</html>

````

## 前端参考手册

- [Layui - 经典开源模块化前端 UI 框架](https://www.layui.com/)

- [jQuery插件库-收集最全最新最好的jQuery插件 (jq22.com)](https://www.jq22.com/)

- [Illustrations | unDraw](https://undraw.co/illustrations)插画素材库

- [Emoji Island | Download Emoji Images For Free!](https://emojiisland.com/)

- [CodePen](https://codepen.io/)

- 配色[Grabient](https://www.grabient.com/)

- https://fontawesome.dashgame.com/

- [Coolors - The super fast color schemes generator!](https://coolors.co/)

  



