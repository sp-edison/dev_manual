

# matplotlib 사용시 아래와 같은 에러가 발생한다면


```bash
The main problem is that (on your system) matplotlib chooses an x-using backend by default. I just had the same problem on one of my servers. The solution for me was to add the following code in a place that gets read  before  any other pylab/matplotlib/ pyplot  import:
```
matplotlib import 이후 ```matplotlib.use('Agg') ```코드를 추가해 에러를 해결할 수 있습니다.

```Python
import numpy, scipy, math, matplotlib
matplotlib.use('Agg')  <-- 코드 추가
import matplotlib.pyplot as plt
```
