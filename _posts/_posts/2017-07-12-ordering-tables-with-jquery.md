---
id: 11205
title: 'Ordering tables with jquery'
date: '2017-07-12T13:04:10+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.com/?p=11205'
permalink: /11205/
categories:
    - 'Web Development'
tags:
    - jquery
    - web
---

Last spring I was organizing official Finnish ice climbing championships[ www.finice.com](http://www.finice2017.com/) . We were a really small team behind this production. The problem for us was how to deliver real time results to the audience, and for the media broadcast company, which was filming and commenting the competition.  
I wrote a small script to order the results, which I just quickly entered to the html page during the competition.

```
function sortTable(table_id, sortColumn){
    var tableData = document.getElementById(table_id).getElementsByTagName('tbody').item(0);
    var rowData = tableData.getElementsByTagName('tr');
    for(var i = 0; i &lt; rowData.length - 1; i++){
        for(var j = 0; j &lt; rowData.length - (i + 1); j++){
            if(Number(rowData.item(j).getElementsByTagName('td').item(sortColumn).innerHTML.replace(/[^0-9\\.]+/g, '')) &lt; Number(rowData.item(j+1).getElementsByTagName('td').item(sortColumn).innerHTML.replace(/[^0-9\\.]+/g, ''))){
                tableData.insertBefore(rowData.item(j+1),rowData.item(j));
            }
        }
    }
    tableData = document.getElementById(table_id).getElementsByTagName('tbody').item(0);
    rowData = tableData.getElementsByTagName('tr');
    for(var i = 0; i &lt;= rowData.length - 1; i++){
        //console.log(rowData.item(i).getElementsByTagName('td').item(0));
        rowData.item(i).getElementsByTagName('td').item(0).innerHTML = i+1;
    }
}
```

  
The main idea was to call this sorttable during the competition, and just remove it afterwards, when I had written the official results to the page.  
Calling the table sorter was pretty easy. Just sort the document, on document.ready.    

```
    $( document ).ready(function() {
     sortTable('men', 4);
     sortTable('women', 4);
    });
```