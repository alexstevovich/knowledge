
# Stop Process Running on Port

 
## Step 1
```

tasklist \ findstr node

```
Will give you the PID (Process ID) of all processes using the port 

## Step 2
```

taskkill /PID <PID> /F

```
Run this for each oneo replace < PID > with the process ID from above step 1