You can use the **Task Scheduler** in Windows to shut down your computer at a specific time, but first, you'll need to create a task with the shutdown command. Here's how you can do this:

### Step-by-Step Guide to Schedule a Shutdown:

1. **Create a Shutdown Command**:
   Open **Command Prompt** as an administrator and type the following command to shut down the computer:
   ```cmd
   shutdown /s /f /t 0
   ```
   - `/s` tells the system to shut down.
   - `/f` forces running applications to close.
   - `/t 0` specifies the time delay in seconds (0 means no delay).

2. **Schedule the Shutdown with Task Scheduler**:

   a. Open **Task Scheduler** by searching for it in the Start menu and selecting **Task Scheduler**.

   b. In the **Task Scheduler**, click on **Create Basic Task** in the right-hand menu.

   c. **Name the Task** (e.g., "Shutdown Computer") and click **Next**.

   d. Select **Daily**, **Weekly**, or **One Time**, depending on when you want the shutdown to occur, then click **Next**.

   e. Set the exact **time** you want the computer to shut down, then click **Next**.

   f. Select **Start a Program** and click **Next**.

   g. In the **Program/Script** field, enter:
      ```cmd
      shutdown
      ```

      And in the **Add arguments** field, enter:
      ```cmd
      /s /f /t 0
      ```

   h. Click **Next**, review your task, and then click **Finish**.

### Example Command in Task Scheduler:
- **Program/Script**: `shutdown`
- **Add Arguments**: `/s /f /t 0`

This will schedule your computer to shut down at the time you specify.

### Using Command Line (Without Task Scheduler):
Alternatively, you can create the scheduled task from the **Command Prompt** by using the `schtasks` command. Here's an example:

```cmd
schtasks /create /tn "ShutdownComputer" /tr "shutdown /s /f /t 0" /sc once /st 14:30
```

This command will create a task named "ShutdownComputer" that will execute the shutdown command at **2:30 PM**.

- `/tn "ShutdownComputer"` – Specifies the task name.
- `/tr "shutdown /s /f /t 0"` – Specifies the command to execute.
- `/sc once` – Schedules the task to run once.
- `/st 14:30` – Specifies the time (24-hour format).

You can change the time in the `"/st"` argument to the specific time you want to schedule the shutdown.

The command you provided will create a scheduled task named **"CostSavingsShutdownComputer01"** to shut down the computer at **14:30 (2:30 PM)**. Here's a breakdown of the command:

```cmd
schtasks /create /tn "CostSavingsShutdownComputer01" /tr "shutdown /s /f /t 0" /sc once /st 14:30
```

### Explanation of the Command:
- `/create` – Creates a new scheduled task.
- `/tn "CostSavingsShutdownComputer01"` – Names the task **CostSavingsShutdownComputer01**.
- `/tr "shutdown /s /f /t 0"` – Specifies the program/command to execute. In this case, it's the **shutdown** command with the flags:
  - `/s` to shut down the system.
  - `/f` to force running applications to close.
  - `/t 0` to set the timeout to 0 seconds (immediate shutdown).
- `/sc once` – Schedules the task to run **once**.
- `/st 14:30` – Specifies the start time as **14:30 (2:30 PM)** in **24-hour format**.

### How to Use It:
1. Open **Command Prompt** as **Administrator** (important to ensure you have the necessary permissions).
2. Paste and run the command.
3. After executing the command, the scheduled task will be created.

The computer will shut down automatically at **2:30 PM** on the date the task is set.

### To Check If the Task Was Created:
You can list all scheduled tasks to confirm the task was created by running:

```cmd
schtasks /query
```

If you need to modify or delete the task later, you can use the following commands:

- **To delete the task:**
  ```cmd
  schtasks /delete /tn "CostSavingsShutdownComputer01"
  ```

- **To view details of the task:**
  ```cmd
  schtasks /query /tn "CostSavingsShutdownComputer01"
  ```
If you'd like to schedule the shutdown task to run **daily** at a specific time, you can modify the command by changing the `/sc` parameter from `once` to `daily`. 

Here’s how you can set it up for **daily** shutdown at **14:30 (2:30 PM)**:

### Command for Daily Shutdown:

```cmd
schtasks /create /tn "CostSavingsShutdownComputer01" /tr "shutdown /s /f /t 0" /sc daily /st 14:30
```

### Breakdown of the Command:
- `/sc daily` – Schedules the task to run **every day** at the specified time.
- `/st 14:30` – Specifies the start time as **14:30 (2:30 PM)** in **24-hour format**.

### How It Works:
- The task will run **every day** at **2:30 PM** and will initiate a shutdown of the system.
- It will use the same `shutdown /s /f /t 0` command to shut down the system immediately, forcing all applications to close.

### Example Use Case:
If you want to shut down the system at 2:30 PM every day, this command will schedule it once, and the system will automatically perform the shutdown each day at that time.

### Check If the Task Was Created:
You can list all scheduled tasks to confirm by running:

```cmd
schtasks /query
```

This will show you all tasks currently scheduled on your system, and you can check if **CostSavingsShutdownComputer01** is listed.
