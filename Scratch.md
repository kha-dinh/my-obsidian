

```
// BASELINE
Concurrency Level:      10
Time taken for tests:   8.770 seconds
Complete requests:      1000
Failed requests:        0
Non-2xx responses:      1000
Total transferred:      494000 bytes
HTML transferred:       341000 bytes
Requests per second:    114.03 [#/sec] (mean)
Time per request:       87.699 [ms] (mean)
Time per request:       8.770 [ms] (mean, across all concurrent requests)
Transfer rate:          55.01 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:       36   78  72.0     41     509
Processing:     0    8  33.8      0     298
Waiting:        0    8  33.8      0     298
Total:         37   87  87.0     43     661

Concurrency Level:      50
Time taken for tests:   87.088 seconds
Complete requests:      10000
Failed requests:        0
Non-2xx responses:      10000
Total transferred:      4940000 bytes
HTML transferred:       3410000 bytes
Requests per second:    114.83 [#/sec] (mean)
Time per request:       435.439 [ms] (mean)
Time per request:       8.709 [ms] (mean, across all concurrent requests)
Transfer rate:          55.39 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:       36  309 372.7    154    2881
Processing:     0  125 224.3     11    2104
Waiting:        0  125 224.3     11    2103
Total:         36  434 503.8    224    3718

Concurrency Level:      10
Time taken for tests:   9.627 seconds
Complete requests:      1000
Failed requests:        0
Non-2xx responses:      1000
Total transferred:      494000 bytes
HTML transferred:       341000 bytes
Requests per second:    103.87 [#/sec] (mean)
Time per request:       96.274 [ms] (mean)
Time per request:       9.627 [ms] (mean, across all concurrent requests)
Transfer rate:          50.11 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:       36   87  76.2     50     586
Processing:     0    9  31.9      0     330
Waiting:        0    8  31.9      0     330
Total:         37   95  86.7     54     605
```