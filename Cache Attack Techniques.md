
[[Cache Attacks]] techniques  combines different actions (evict cache / priming / probing / timing) to get the desired information, usually whether  a cache set ([[Set-associative Caches]]) has been accessed by the victim or not . 
- [[Evict + Time]] 
- [[Prime + Probe]] 
- [[Flush + Reload]] 
- [[Evict + Reload]]
- [[Flush + Flush]]
- [[Invalidate + Transfer]]
- [[@briongos2021aim|CacheSnipper]]
- [[Prime + Abort]]
- [[Prime + Probe]] and [[Flush + Reload]] are most used. Prime + Probe requires little attack requirement, while Flush + reload provides precise information.
	- Both attacks requires a precise timers, but can also be bypassed with [[Intel TSX]]
- [[@gruss2015cache|Cache Template Attack]]


