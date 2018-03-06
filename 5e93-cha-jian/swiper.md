### 

### 一、在vue-cli中使用：

1. 安装：npm install swiper -save
2. 代码示例：

```
<template>
    <div>
        <h2>Swiper test</h2>
        <!-- Slider main container -->
        <div class="swiper-container">
            <!-- Additional required wrapper -->
            <div class="swiper-wrapper">
                <!-- Slides -->
                <div class="swiper-slide">Slide 1</div>
                <div class="swiper-slide">Slide 2</div>
                <div class="swiper-slide">Slide 3</div>
                ...
            </div>
            <!-- If we need pagination -->
            <div class="swiper-pagination"></div>

            <!-- If we need navigation buttons -->
            <div class="swiper-button-prev"></div>
            <div class="swiper-button-next"></div>

            <!-- If we need scrollbar -->
            <div class="swiper-scrollbar"></div>
        </div>
    </div>
</template>

<script>
    import Swiper from 'swiper'
    import 'swiper/dist/css/swiper.min.css'
    export default {
        name: 'Swiper',
        mounted () {
            // 此注释可用于取消mySwiper未被使用的报错
            /* eslint-disable no-unused-vars */
            var mySwiper = new Swiper('.swiper-container', {
                loop: true
            })
        }
    }
</script>

<style scoped>

</style>
```



