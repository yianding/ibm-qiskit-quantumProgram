```python
import numpy as np
# Importing standard Qiskit libraries
from qiskit import QuantumCircuit, transpile, Aer, IBMQ
from qiskit.tools.jupyter import *
from qiskit.visualization import *
from ibm_quantum_widgets import *

# Loading your IBM Quantum account(s)
IBMQ.delete_account()
IBMQ.save_account('582f2e39c7d737826d394062d37a18b680d265b5b28ed31674168e7bcc9fa01ad19470abd52d3cd9e2645e9c850e50596e0f36caca6c673f2487fb9a4403fb58')
provider = IBMQ.load_account()
```


```python
from qiskit import *
circuit = QuantumCircuit(2,2)
```


```python
circuit.draw(output='mpl')
```




![png](output_2_0.png)




```python

#在0号量子比特上增加一个H门
circuit.h(0)
circuit.h(1)
#把0,1号两个量子比特进行纠缠
circuit.cx(0,1) # order is control, target
#测量0,1量子比特的结果,测量结果保存在0,1号经典比特中去
circuit.measure([0,1], [0,1]) 
#画出电路图
circuit.draw(output='mpl')

```




![png](output_3_0.png)




```python
simulator = Aer.get_backend('qasm_simulator')
```


```python

result = execute(circuit, backend=simulator).result()
```


```python

from qiskit.visualization import plot_histogram
plot_histogram(result.get_counts(circuit))
```




![png](output_6_0.png)




```python

qcomp = provider.get_backend('ibmqx2')
```


```python

job = execute(circuit, backend=qcomp)

```


```python

result = job.result()
plot_histogram(result.get_counts(circuit))
```




![png](output_9_0.png)




```python

```


```python

```
