# jQuery

1. Datatable 組件

``` text
http://localhost:50465//Home/AjaxGetJsonData?draw=1&columns[0][data]=Name&columns[0][name]=&columns[0][searchable]=true&columns[0][orderable]=true&columns[0][search][value]=&columns[0][search][regex]=false&columns[1][data]=Age&columns[1][name]=&columns[1][searchable]=true&columns[1][orderable]=false&columns[1][search][value]=&columns[1][search][regex]=false&columns[2][data]=DoB&columns[2][name]=&columns[2][searchable]=true&columns[2][orderable]=true&columns[2][search][value]=&columns[2][search][regex]=false&order[0][column]=0&order[0][dir]=asc&start=0&length=10&search[value]=&search[regex]=false&_=1437225574923
```

返回json
```json
{
    "draw":1,
    "recordsTotal":995,
    "recordsFiltered":995,
    "data":[
        {"Name":"Name_00001","Age":"107","DoB":"06/14/1908"},
        {"Name":"Name_00002","Age":"41","DoB":"05/09/1974"},
        …
        {"Name":"Name_00010","Age":"45","DoB":"06/11/1970"}
    ]
}
```

c# model for jsonResult
```cs
public class DataTableData
{
    public int draw { get; set; }
    public int recordsTotal { get; set; }
    public int recordsFiltered { get; set; }
    public List<T> data { get; set; }
}
```