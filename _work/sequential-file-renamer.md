---
short_name: sequential-file-renamer
name: Sequential File Renamer
description: Simple C# script to take files from one directory and put them in another with sequential file names. 
date: 23.03.2020
layout: work
---

{{page.description}}

I used this when importing image sequences into Sony Vegas for timelapse videos. If the files aren't named sequentially then Vegas won't recognise it.

```csharp
using System;
using System.IO;

namespace SequentialFileRenamer
{
    class Program
    {
        static void Main(string[] args)
        {
            const string INPUT_DIR = @"";
            const string OUTPUT_DIR = @"";

            DirectoryInfo di = new DirectoryInfo(INPUT_DIR);
            FileInfo[] images = di.GetFiles("*.png");

            int filename = 1;
            foreach (var image in images)
            {
                File.Copy(image.FullName, OUTPUT_DIR + filename + ".png");
                Console.WriteLine(filename + " created.");
                filename++;
            }
        }
    }
}

```