# TransactionScope.Complete Maybe
During a training class this week I learned that the `Complete()` method in the `TransactionScope` class works different from what I have always thought. I've always thought that when you issue a call to the `Complete()` method the transaction is either committed or you get an exception if the transaction cannot be committed. In my mind once the call to `Complete()` returned it was a sure bet that the transaction was successfully committed. It turns out that is not necessarily true.

The following code snippet shows a typical usage of `TransactionScope` when connecting to a SQL Server database. The steps are basically start a transaction, issue a few SQL commands, and call the complete method to commit the transaction. In a real application you will have more than one SQL Command and perhaps nested transactions but the idea is pretty much the same.

```code
using (TransactionScope tx = new TransactionScope())
{
  using (SqlConnection conn = new SqlConnection(connString))
  {
    conn.Open();
    string sql ="INSERT INTO MyTable(ID,Name) VALUES(1,'Test')";
    SqlCommand command = new SqlCommand(sql, conn);
    command.ExecuteNonQuery();
  } // conn

  Console.WriteLine("INSERT command has been issued but not committed.");
  Console.WriteLine("Stop SQL Server and press [ENTER] to continue...");
  Console.ReadLine();
  tx.Complete();
  Console.WriteLine("Yikes! tx.Complete() didn't throw an exception even though SQL Server has been stopped.");
  Console.WriteLine("Press [ENTER] to continue...");
  Console.ReadLine();
} // tx
```

In this particular example however I am purposely forcing an error condition by pausing the program right before the call to `Complete()`, then manually shutting down SQL Server, and finally letting the program continue its execution. This is definitively not something that you will do in an application but the point of this example is to emulate what happens if the server goes down right before the call to `tx.Complete()`. My thought was that the program will throw an exception on the call to `tx.Complete()` but to my surprise that was not the case. The call to `tx.Complete()` executed and came back with no indication that an error has happened. Below is the output that this program gave me:

![tx.Complete didn't throw exception](https://hectorcorrea.com/images/txComplete.jpg)

Notice how the lines after `tx.Complete()` were executed which means that no Exception was thrown even though SQL Server was down at the time of the call! How come this is possible? Does this mean that I have no way of knowing that the transaction succeeded or failed. This is kind of a big deal.

It turns out the real issue here is that the `Complete()` method does not work quite the way I thought it did. Here is what what [MSDN](http://msdn.microsoft.com/en-us/library/system.transactions.transactionscope.complete.aspx) says:

> When you are satisfied that all operations within the scope are completed successfully, you should call this method only once to inform that transaction manager that the state across all resources is consistent, and the transaction can be committed. It is very good practice to put the call as the last statement in the using block. [...] The actual work of commit between the resources manager happens at the End Using statement if the TransactionScope object created the transaction. If it did not create the transaction, the commit occurs whenever Commit is called by the owner of the CommittableTransaction object. At that point the Transaction Manager calls the resource managers and informs them to either commit or rollback, based on whether this method was called on the TransactionScope object.

Notice that it clearly says you call this method to **inform** the transaction manager that the transaction can be committed. The actual commit happens at the end using statement. Indeed, if I let the program continue its execution I do get an exception when I reach to the end of the using statement. Below is an example of the Exception that I got:

![Exception was thrown here](https://hectorcorrea.com/images/txCompleteEx.jpg)

With this knowledge, let's review what happened when the line `tx.Complete()` was executed and SQL Server was already shutdown. The call to `tx.Complete()` informed the transaction manager that as far as we were concerned the transaction could be committed. This is why that line executed with no problems. Next, when the transaction scope reached the end using statement and it tried to commit it detected that something was wrong and threw an exception indicating that **"the transaction is in doubt"**. There was also an inner exception that elaborated that a "transport-level error has occurred" in this case as a result of .NET not being able to reach SQL Server to confirm if indeed SQL Server committed the transaction or not. The best `TransactionScope` could do is doubt it. 

This is actually really good. If a similar situation where to happen in a production environment I would doubt that the transaction was committed too. In this particular example I know for sure it wasn't committed since I shutdown SQL Server at the right moment, but in real application there wouldn't be a way for us to know if we lost connectivity with SQL before or after the commit command was sent. For example, let's say that SQL Server didn't go down but rather that our program lost network connectivity with it. In that case we couldn't confirm that SQL Server committed the transaction but SQL Server might have received the commit command just before we lost connectivity and indeed committed the transaction successfully. In that case the best `TransactionScope` can do is doubt it and that's as correct as you can ask for.

To make matters more interesting you can use `TransactionScope` to handle nested transactions and transactions against resources other than databases. I am glad to know that whoever wrote this code in the framework already thought of these conditions so that I don't have to. Check out the MDSN documentation for the [TransactionScope](http://msdn.microsoft.com/en-us/library/system.transactions.transactionscope.aspx) class and on [Writting Transactional Applications](http://msdn.microsoft.com/en-us/library/ms229973.aspx) for more information.