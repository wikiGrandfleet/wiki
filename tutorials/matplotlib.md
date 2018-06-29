<!-- TITLE: Matplotlib -->
<!-- SUBTITLE: A quick summary of Matplotlib -->

##### Simple Pie Chart
```python
# Data obtained from https://trends.builtwith.com/web-server on Jan 06, 2017
import matplotlib.pyplot as plt
plt.figure(figsize=(4,4))

x = [0.31,0.3,0.14,0.1,0.15]
labels = ['nginx','Apache','IIS','Varnish','Others']
plt.pie(x,labels=labels,autopct='%1.1f%%')
plt.title('Web Server Usage Statistics')
plt.show()
```