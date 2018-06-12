# Elastic Searach - help

## 匹配
- ### 匹配全部
    * query
    ```
    {
        "query":{
            "match_all":{}
        }
    }
    ```
    
- ### 完全匹配
    * query
    ```
    GET /my_index/my_type/_search
    {
        "query": {
            "match": {
                "title": "QUICK!"
            }
        }
    }
    ```

- ### 模糊匹配
    * query
    ```
    GET /my_index/my_type/_search
    {
        "query": {
            "match_phrase": {
                "title": "quick brown fox"
            }
        }
    }
    ```
    ```
    GET /my_index/my_type/_search
    {
        "query": {
            "match_phrase-prefix": {
                "title": "quick brown fox"
            }
        }
    }
    ```

## 过滤器
- ### term过滤器
    置入其他过滤器中，filter或must类的都可

    * query
    ```
    GET /my_store/products/_search
    {
        "query" : {
            "filter" : {
                { "term" : {"price" : 20}}, 
                { "term" : {"productID" : "XHDK-A-1293-#fJ3"}} 
            }
        }
    }
    ```

- ### range范围过滤器
    同term：
    ```
    gt: > 大于（greater than）
    lt: < 小于（less than）
    gte: >= 大于或等于（greater than or equal to）
    lte: <= 小于或等于（less than or equal to）
    ```

    * query
    ```
    GET /my_store/products/_search
    {
        "query" : {
            "filter" : {
                "range" : {
                    "price" : {
                        "gte" : 20,
                        "lt"  : 40
                    }
                }, 
                { "term" : {"productID" : "XHDK-A-1293-#fJ3"}} 
            }
        }
    }
    ```

- ### bool过滤器
    复合过滤器，内部嵌套别的过滤器

- ### must过滤器
    严格匹配
    * query
    ```
    GET /my_index/my_type/_search
    {
        "query": {
            "bool": {
                "must": {
                    "match": {
                        "title": "quick"
                    }
                },
            }
        }
    }
    ```

- ### must_not
    严格不匹配
    * query
    ```
    GET /my_index/my_type/_search
    {
        "query": {
            "bool": {
                "must_not": {
                    "match": {
                        "title": "lazy"
                    }
                },
            }
        }
    }
    ```
    
- ### should
    或的使用
    * query
    ```
    GET /my_index/my_type/_search
    {
        "query": {
            "bool": {
                "should": [
                    { "match": { "title": "brown" }},
                    { "match": { "title": "dog"   }},
                    { "bool":  {
                        "should": [
                            { "match": { "translator": "Constance Garnett" }},
                            { "match": { "translator": "Louise Maude"      }}
                        ]
                    }
                    }
                ]
            }
        }
    }
    ```

- ### 组合使用
    * query
    ```
    GET /my_index/my_type/_search
    {
        "query": {
            "bool": {
                "must":       { "match": { "title": "quick" }},
                "must_not":   { "match": { "title": "lazy"  }},
                "should": [
                    { "match": { "title": "brown" }},
                    { "match": { "title": "dog"   }},
                    { "bool":  {
                        "should": [
                            { "term" : {"price" : 20}},
                            { "match": { "translator": "Louise Maude"      }}
                        ]
                    }
                    }
                ]
            }
        }
    }
    ```

## 排序
    按字段的值进行排序,可有优先级
   * query

    ```
    GET /my_index/my_type/_search
    {
        "sort": [
            {
            "FIELD": {
                "order": "asc"
            },
            {
            "FIELD": {
                "order": "desc"
            }
        ]
    }
    ```

## 显示字段
    只显示固定字段

   * query : 不显示

    ```
    GET /_search
    {
        "_source": false,
        "query" : {
            "term" : { "user" : "kimchy" }
        }
    }
    ```

   * query : 匹配字段显示

    ```
    GET /_search
    {
        "_source": "obj.*",
        "query" : {
            "term" : { "user" : "kimchy" }
        }
    }
    ```

   * query : 多个匹配字段显示

    ```
    GET /_search
    {
        "_source": [ "obj1.*", "obj2.*" ],
        "query" : {
            "term" : { "user" : "kimchy" }
        }
    }
    ```

   * query : 排除字段显示

    ```
    GET /_search
    {
        "_source": {
            "includes": [ "obj1.*", "obj2.*" ],
            "excludes": [ "*.description" ]
        },
        "query" : {
            "term" : { "user" : "kimchy" }
        }
    }
    ```