### video
#### 视频自动播放
```html
<div class="video-div">
    <video id="play" controls autoplay="autoplay" preload="auto">
        <source src="video/1.mp4" type="video/mp4">
        抱歉，您的浏览器不支持内嵌视频
    </video>
</div>
```
1、浏览器支持则自动播放，不支持则静音播放
```javascript
window.onload = function () {
       var player = document.getElementById('play');
       var playPromise = player.play() || Promise.reject('');
       playPromise.then(function(){
           // Video could be autoplayed, do nothing.
       }).catch(function () {
           // Video couldn't be autoplayed because of autoplay policy. Mute it and play.
           player.muted = true;
           player.play();
       });
 }
```

2、通过用户交互来打开音乐
```javascript
window.onload=function () {
        var player=document.getElementById('play');
        document.body.addEventListener('mousedown', function(){
            player.muted=false
        })
}
```
3、换浏览器
360、IE都可以自动播放


#### video/audio兼容性
[MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Supported_media_formats)

#### 事件
|  事件   | 描述  |
|  :----  | :----  |
| loadstart | 在媒体开始加载时触发
| durationchange |元信息已载入或已改变，表明媒体的长度发生了改变。例如，在媒体已被加载足够的长度从而得知总长度时会触发这个事件。
| loadedmetadata |媒体的元数据已经加载完毕，现在所有的属性包含了它们应有的有效信息
| loadeddata | 媒体的第一帧已经加载完毕
| progress | 告知媒体相关部分的下载进度时周期性地触发。有关媒体当前已下载总计的信息可以在元素的buffered属性中获取到
| canplay | 可以播放，但中途可能因为加载而暂停
| canplaythrough |	表示资源缓冲完毕，可以播放
| durationchange |	资源长度改变，执行一次
| play |	资源实际开始播放，autoplay和play()都会触发play事件
| playing |	同上 执行一次
| pause |	当视频已暂停时
| ended |	结束时触发 loop时不触发该事件
| seeking | 在跳跃操作开始时
| seeked | 在跳跃操作完成时
| volumechange | 在音频音量改变时触发（既可以是volume属性改变，也可以是muted属性改变）

注：视频/音频加载过程中，事件触发顺序：onloadstart -> canplaythrough

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