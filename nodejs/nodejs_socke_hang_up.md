
项目中需要在node里请求tomcat数据，为了方便，请求参数整成URL，使用http.get请求tomcat server数据，量上来之后总是偶尔会报**socket hang up**的异常.

`
var req = http.get(url, function(res){...})
`

系统tcp参数、tomcat参数各种设置，http maxSockets各种调都不行。

绝望之际，换成post方式提交，然后幸福来了，不再报了。不过还没深究其原理。

    var options = {
        host: host,
        port: 80,
        path: path,
        method: 'POST',
        headers: {
            'Content-Type': 'application/x-www-form-urlencoded',
            'Content-Length': Buffer.byteLength(data)
        }
    };
    
    var req = http.request(options, function(res) { ...});

    req.write(data);
    req.end();
    


