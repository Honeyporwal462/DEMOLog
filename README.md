|#|Log Error Scanerio|Log Error Description|
|--|--|--|
|1.|Connectivity Issue |Connection error occured<br>Traceback (most recent call last):<br>File "C:\Users\hhoney\PycharmProjects\pythonProject1\venv\lib\site-packages\urllib3\connection.py", line 160, in _new_conn<br>(self._dns_host, self.port), self.timeout, **extra_kw<br>File "C:\Users\hhoney\PycharmProjects\pythonProject1\venv\lib\site-packages\urllib3\util\connection.py", line 61, in create_connection<br>for res in socket.getaddrinfo(host, port, family, socket.SOCK_STREAM<br>File "C:\Users\hhoney\AppData\Local\Programs\Python\Python37-32\lib\socket.py", line 748, in getaddrinfo<br>for res in _socket.getaddrinfo(host, port, family, type, proto, flags):<br>socket.gaierror: [Errno 11001] getaddrinfo failed|
|2|Wrong Credentials -Oneclick Server|Getting error response while getting subscriptionId from Spectrum API with status code 401<br>2020-10-05 17:13:56,213: ERROR: 369: Error in script execution<br>Traceback (most recent call last):<br>File "invoke.py", line 358, in main<br>logger.debug("subscription id is :" + subscriptionId)<br>TypeError: can only concatenate str (not "NoneType") to str|
|3|Wrong Credentials - <br>PDXC|Getting error response from PDXC API with status code 403|
|4|PullAlarmsSubscription file is missing|ERROR: 306: Getting error from Spectrum API while getting subscriptionId<br>Traceback (most recent call last):<br>File "invoke.py", line 276, in subscribeAlarm<br>file = open('PullAlarmsSubscriptionn.xml', 'r')<br>FileNotFoundError: [Errno 2] No such file or directory: 'PullAlarmsSubscriptionn.xml'|
