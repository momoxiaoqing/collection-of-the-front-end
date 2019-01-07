### jQuery注意事项

#### index()

$(el).index()

$(el2).index($(el))

```
    <div class="list-1">
        <div class="list-2"></div>
        <div class="list-2"></div>
    </div>
    <div class="list-1">
        <div class="list-2" id="test"></div>
        <div class="list-2"></div>
    </div>

    $('#test').index() // 0
    $('.list2').index('#test') //2
```