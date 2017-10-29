# Datatable 组件

1. option searchDelay 设置搜索延迟时间
参数详解连接 [searchDelayOption](https://datatables.net/reference/option/searchDelay) [searchDelay](http://datatables.club/manual/daily/2016/05/11/option-searchDelay.html)

Datatables 的客户端搜索和服务器搜索默认的延迟时间是400ms，所以当按下键后就立马开始搜索， 这样处理只是符合大多数情况，但是有些时候这样处理太消耗资源，降低了用户体验：
> 1. 电脑比较旧了，性能更不上，那么需要调整下这个延迟时间
> 2. 服务器端数据太多了，减少请求次数，这是优化服务器性能
> 3. 减少重绘次数
> 4. 当然，你还可以设置为0，来获得更快的速度，只要你愿意

接受的参数是以 ms 为单位

设置延时时间为350ms

``` js
var table = $('#example').DataTable( {
   searchDelay: 350
 } );
```

2. 延迟搜索,直到输入3个字符或点击一个按钮
```js 
// Call datatables, and return the API to the variable for use in our code
// Binds datatables to all elements with a class of datatable
var dtable = $(".datatable").dataTable().api();

// Grab the datatables input box and alter how it is bound to events
$(".dataTables_filter input")
    .unbind() // Unbind previous default bindings
    .bind("input", function(e) { // Bind our desired behavior
        // If the length is 3 or more characters, or the user pressed ENTER, search
        if(this.value.length >= 3 || e.keyCode == 13) {
            // Call the API search function
            dtable.search(this.value).draw();
        }
        // Ensure we clear the search if they backspace far enough
        if(this.value == "") {
            dtable.search("").draw();
        }
        return;
    });
```

``` js
$(function(){
  var myTable=$('#myTable').dataTable();

  $('.dataTables_filter input')
    .unbind('keypress keyup')
    .bind('keypress keyup', function(e){
      if ($(this).val().length < 3 && e.keyCode != 13) return;
      myTable.fnFilter($(this).val());
    });
});
```

3. 添加按钮/超链接 在列内

[using jquery datatable with asp.net core](http://www.c-sharpcorner.com/article/using-jquery-datatables-grid-with-asp-net-core-mvc/)

```
<script>  
  
        $(document).ready(function ()  
        {  
            $("#example").DataTable({  
                "processing": true, // for show progress bar  
                "serverSide": true, // for process server side  
                "filter": true, // this is for disable filter (search box)  
                "orderMulti": false, // for disable multiple column at once  
                "ajax": {  
                    "url": "/DemoGrid/LoadData",  
                    "type": "POST",  
                    "datatype": "json"  
                },  
                "columnDefs":  
                [{  
                    "targets": [0],  
                    "visible": false,  
                    "searchable": false  
                }],  
                "columns": [  
                    { "data": "CustomerID", "name": "CustomerID", "autoWidth": true },  
                    { "data": "Name", "name": "Name", "autoWidth": true },  
                    { "data": "Address", "name": "Address", "autoWidth": true },  
                    { "data": "Country", "name": "Country", "autoWidth": true },  
                    { "data": "City", "name": "City", "autoWidth": true },  
                    { "data": "Phoneno", "name": "Phoneno", "autoWidth": true },  
                    {  
                        "render": function (data, type, full, meta)  
                        { return '<a class="btn btn-info" href="/DemoGrid/Edit/' + full.CustomerID + '">Edit</a>'; }  
                    },  
                    {  
                        data: null, render: function (data, type, row)  
                        {  
                            return "<a href='#' class='btn btn-danger' onclick=DeleteData('" + row.CustomerID + "'); >Delete</a>";  
                        }  
                    },  
                ]  
  
            });  
        });  
  
  
    function DeleteData(CustomerID)  
        {  
            if (confirm("Are you sure you want to delete ...?"))  
            {  
                Delete(CustomerID);  
            }  
            else  
            {  
                return false;  
            }  
        }  
  
  
        function Delete(CustomerID)  
    {  
        var url = '@Url.Content("~/")' + "DemoGrid/Delete";  
  
            $.post(url, { ID: CustomerID }, function (data)  
                {  
                    if (data)  
                    {  
                        oTable = $('#example').DataTable();  
                        oTable.draw();  
                    }  
                    else  
                    {  
                        alert("Something Went Wrong!");  
                    }  
                });  
    }  
  
</script>
```

4. Advance Search
[Grid with Server Side Advanced Search using JQuery DataTables in ASP.NET MVC 5](https://www.codeproject.com/Articles/1170086/Implement-Grid-with-Server-Side-Advanced-Search-us)

5. Column format

