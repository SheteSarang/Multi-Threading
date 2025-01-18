# Multi-Threading
case-1 1. Dialog with Message:
Show a dialog to the user with a message.
Close the dialog automatically after 15 seconds if the user hasn’t interacted with it.
If the user manually closes the dialog, don’t close it again at the timeout.
using System;
using System.Timers;
 
class Program1
{
    static Timer autoCloseTimer;
 
    static void Main()
    {
        Console.WriteLine("Dialog shown to the user.");
        autoCloseTimer = new Timer(15000);
        autoCloseTimer.Elapsed += delegate
        {
            Console.WriteLine("Closing the dialog automatically.");
            autoCloseTimer.Stop();
        };
        autoCloseTimer.Start();
 
        Console.WriteLine("Press any key to close the dialog manually.");
        Console.ReadKey();
        Console.WriteLine("Dialog closed manually by the user.");
        autoCloseTimer.Stop();
    }
}
case:2Abort Long Operation:
Start a long operation (e.g., a process or a task).
If the operation takes more than 5 seconds, cancel or stop it.
If it finishes within 5 seconds, let it complete normally.
using System;
using System.Diagnostics;
using System.Threading;
 
class Program2
{
    static void Main()
    {
        Console.WriteLine("Starting a long operation...");
 
        Thread longOperationThread = new Thread(() =>
        {
            for (;;)
            {
                // Simulate a long-running task
            }
        });
 
        Stopwatch stopwatch = new Stopwatch();
 
        stopwatch.Start();
        longOperationThread.Start();
 
        while (stopwatch.ElapsedMilliseconds < 5000)
        {
            if (!longOperationThread.IsAlive)
            {
                Console.WriteLine("Operation completed successfully.");
                stopwatch.Stop();
                return;
            }
        }
 
        longOperationThread.Abort();
        stopwatch.Stop();
        Console.WriteLine("Operation aborted after 5 seconds.");
    }
}
3. "In Progress" Popup:
Show a popup saying "In Progress" during a long operation.
Wait 1 second before showing the popup.
If the operation finishes within 1 second, don’t show the popup at all (to avoid "blinking").
If the operation is still running after 1 second, show the popup until the operation is done.using 
using System;
using System.Threading;
 
class Program3
{
    static void Main()
    {
        Console.WriteLine("Starting the task...");
        int taskTime = 3000;
        Thread.Sleep(taskTime);
 
        if (taskTime < 1000)
        {
            Console.WriteLine("Task completed in less than 1 second.");
        }
        else
        {
            Console.WriteLine("Task is running...");
            Thread.Sleep(1000);
            Console.WriteLine("1 second has passed.");
            Thread.Sleep(4000);
            Console.WriteLine("Task ended after 5 seconds.");
        }
    }
}
