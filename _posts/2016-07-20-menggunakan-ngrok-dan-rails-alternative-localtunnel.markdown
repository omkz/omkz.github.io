---
published: true
title: Menggunakan Ngrok dan Ruby on Rails(Localtunnel alternative)
layout: post
categories: misc
tags: ngrok
---
waktu itu ingin menunjukan proses pengembangan aplikasi rails kepada klien. mencari localtunnel kok sudah tidak ada, kemudian nemu ngrok ini.

jadi keuntungan menggunakan ngrok ini, kita tidak perlu mendeploy aplikasi rails kita ke server. orang lain dapat mengakses localhost  kita melalui ngrok tunnel. berikut caranya:

```
ngrok http 8080

ngrok by @inconshreveable                                                                                                                               (Ctrl+C to quit)
                                                                                                                                                                        
Tunnel Status                 online                                                                                                                                    
Update                        update available (version 2.1.3, Ctrl-U to update)                                                                                        
Version                       2.0.25/2.1.1                                                                                                                              
Region                        United States (us)                                                                                                                        
Web Interface                 http://127.0.0.1:4040                                                                                                                     
Forwarding                    http://5be603ec.ngrok.io -> localhost:8000                                                                                                
Forwarding                    https://5be603ec.ngrok.io -> localhost:8000                                                                                               
                                                                                                                                                                        
Connections                   ttl     opn     rt1     rt5     p50     p90                                                                                               
                              0       0       0.00    0.00    0.00    0.00       

```

rails s -p 8080

```
ngrok by @inconshreveable                                                                                                                               (Ctrl+C to quit)
                                                                                                                                                                        
Tunnel Status                 online                                                                                                                                    
Version                       2.0.25/2.1.1                                                                                                                              
Region                        United States (us)                                                                                                                        
Web Interface                 http://127.0.0.1:4040                                                                                                                     
Forwarding                    http://8c7cbd29.ngrok.io -> localhost:8080                                                                                                
Forwarding                    https://8c7cbd29.ngrok.io -> localhost:8080                                                                                               
                                                                                                                                                                        
Connections                   ttl     opn     rt1     rt5     p50     p90                                                                                               
                              13      0       0.00    0.00    31.23   66.93                                                                                             
                                                                                                                                                                        
HTTP Requests                                                                                                                                                           
-------------                                                                                                                                                           
                                                                                                                                                                        
GET /sell_horse                304 Not Modified                                                                                                                         
GET /sell_horse                304 Not Modified                                                                                                                         
GET /sell_horse                200 OK                   
```