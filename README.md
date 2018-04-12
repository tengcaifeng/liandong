# 三级联动
## 通过省选择学校的代码网上有很多，也有很多结构化的数据，拿来直接可以用

## 专业数据网上并不多见，我通过scrapy爬了一个高考网站的专业数据，保存成json格式再做成了三级联动效果
### 实现重载功能，因为第一次初始化的时候没有点击事件不传参数的，但是点击select的时候需要传递当前点击的值用来构建第二个下拉列表
<p>关键代码：
<code>
    function initClass_3() {

        var len= arguments.length;//获取传递的参数个数
        var class3_arr = [];//初始化三级专业列表

        if(len == 0){
            var selectedClass2_value = $("#majorClass #select2").val();//获取选的class2的value 0101 0201 0202....

            for (var k in class3) {
                if (k.substr(0, 4) == selectedClass2_value) {
                    class3_arr[k] = class3[k]
                }
            }
        }else if(len ==1){
            class3_arr = arguments[0]//传递了参数获取第一个参数
        }


        var majorULlistr = "" //拼接专业的html代码
        for (var i in class3_arr) {
            // console.log(class2_arr[i])
            if (class3_arr[i] > 13) {
                majorULlistr += "<li class='DoubleWidthLi'>" + class3_arr[i] + "</li>"
            } else {
                majorULlistr += "<li>" + class3_arr[i] + "</li>"
            }
        }
        $(".majorList ul").html(majorULlistr)//拼接学校的html代码
        //学校列表点击事件
        $(".majorList ul li").bind("click", function () {
            $("#majorName").val($(this).html());
            $("#majorClass").hide();
        })
    }

</code></p>
