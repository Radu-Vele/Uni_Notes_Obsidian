# Hazard Detection and Avoidance Unit

## Possible hazard issues:
### 1. Structural

 > [!INFO] Because of resource dependency

Solution:
- independent Instruction and Data memory
- Asynchronous reads
- RF write in the $1^{st}$ half and reads in the $2^{nd}$ half of the clock cycle

### 2. Data

>[!Info] Use data before it's ready
>RAW hazards

Solution:
- Hazard detection
- Forwarding Unit (additional control signals and data is forwarded through the unit that looks pretty much combinational)
	- Special case for Load Data Hazards (need stalls): **Hazard detection unit**
	- instruction reorder (can I do this, not sure tho)

![[Pasted image 20221010085856.png]]



### 3. Control

>[!info] Related to flow control

**Solutions**:
-  flushing
- Branch prediction
- Delay branch slot

> [!Question] Can I use the prediction algorithms