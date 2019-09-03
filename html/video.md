### video
#### 视频自动播放
```
<div class="video-div">
    <video id="play" controls autoplay="autoplay" preload="auto">
        <source src="video/1.mp4" type="video/mp4">
        抱歉，您的浏览器不支持内嵌视频
    </video>
</div>

<script>
    $(function () {
        var player=document.getElementById('play');

        player.oncanplaythrough=function () {
            player.play();
        }
    });
</script>
```

#### video/audio兼容性
[MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Supported_media_formats)

#### 事件
|  事件   | 描述  |
|  :----  | :----  |
| canplaythrough |	表示资源缓冲完毕，可以播放
| durationchange |	资源长度改变，执行一次
| play |	资源实际开始播放，autoplay和play()都会触发play事件
| playing |	同上 执行一次
| pause |	当视频已暂停时
| progress |	资源播放过程中多次执行
| ended |	结束时触发 loop时不触发该事件

#### 属性
|  属性   | 描述  |
|  :----  | :----  |
|currentSrc |	返回资源地址
|currentTime |	设置或返回视频中的当前播放位置（以秒计）
|duration |	返回资源总时长（以秒计）
|paused |	设置或返回视频是否暂停
|ended |	返回视频的播放是否已结束

#### 方法
|  方法   | 描述  |
|  :----  | :----  |
| play() |	播放资源
| pause() |	暂停资源
| load() |	重新加载src指定的资源