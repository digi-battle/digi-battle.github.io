---
short_name: Etsy-Watch-Bot
name: Etsy Watch Bot
description: Hacky and simple bot to check for new items listed on an Etsy store.
date: 05/12/2022
layout: work
---

**This doesn't work since Etsy implemented bot checks and I don't plan on fixing it**

{{page.description}}

I was following a seller but every time they listed something it immediately sold out so I wrote this. The only notification that an item was found is from the console so I just had this program running in the background while I used my PC as normal.

An optimisation would be to have an email alert or even a desktop pop-up when a new item was found.

Written in C# dotnet core using HtmlAgilityPack. 

```csharp
using HtmlAgilityPack;

namespace EtsyWatch
{
    class Program
    {
        public static string EtsyStore = "https://www.etsy.com/shop/SHOPNAMEHERE";
        public static int SleepTimeMs = 6000; 
        public static int QueryCount = 0;
        public static string LogFile = Path.Combine(Environment.CurrentDirectory, "log.txt");

        static void Main()
        {
            bool over = false;
            CheckLogFile();
            WriteLog("WATCH STARTED");

            while (!over)
            {
                QueryCount++;

                if (NewItem())
                {
                    // TODO: Send an email 
                    over = true;
                }
                else
                {
                    WriteLog("NO NEW ITEMS");
                }

                Thread.Sleep(SleepTimeMs);
            }

            WriteLog("NEW ITEM FOUND!!!!!");
        }

        static bool NewItem()
        {
            bool ret = false;
            HtmlWeb web = new HtmlWeb();

            try
            {
                HtmlDocument doc = web.Load(EtsyStore);

                if (!doc.Text.Contains("No items listed at this time"))
                {
                    ret = true;
                }
            }
            catch (Exception ex)
            {
                WriteLog($"ERROR = {ex.Message} \n {ex.StackTrace}");
            }

            return ret;
        }

        static void CheckLogFile()
        {
            if (!File.Exists(LogFile))
            {
                File.Create(LogFile);
            }
        }

        static void WriteLog(string message)
        {
            message = $"{DateTime.Now.ToString()} : ({QueryCount}) : {message}";
            Console.WriteLine(message);

            try
            {
                using StreamWriter file = new StreamWriter(LogFile, append: true);
                file.WriteLine(message);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"\n\n LOG FILE ERROR: {ex.Message} n - {ex.StackTrace} n\n");
            }
        }
    }
}

```