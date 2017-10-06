# First_Project
A Console App written in C# that utilizes Gmail's SMTP host. 

// TITLE: GMAIL CLIENT
// Main Class

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace GmailClient
{
    class Program
    {
        public static int userNum;
        public static string address = "";
        public static string password = "";
        static void Main(string[] args)
        {
            // Do loop for menu selection
            do
            {
                // If else outer statement hides other options before initial log in.
                if (loggedIn(address, password) == false)
                {
                    Menu(1);
                    userNum = Convert.ToInt32(Console.ReadLine());
                    if (userNum == 1)
                    {
                        credentials();
                    }
                    else if (userNum == 2)
                    {
                        break;
                    }
                }
                else
                {
                // Else shell refers to methods
                    Menu(0);
                    userNum = Convert.ToInt32(Console.ReadLine());
                    if (userNum == 1)
                    {
                        credentials();
                    }
                    else if (userNum == 2)
                    {
                        checkMessages();
                    }
                    else if (userNum == 3)
                    {
                        sendMessage();
                    }
                }
            } while (userNum != 4);
        }


        public static void Menu(int num)
        {
            // Description: conditionally displays one of 2 menu variants
            string[] menuLines = new string[8];
            menuLines[0] = "|++++++++++GMAIL CLIENT+++++++++++|";
            menuLines[1] = "|1.) Log In.......................|";
            menuLines[2] = "|2.) Check for new messages.......|";
            menuLines[3] = "|3.) Send a message...............|";
            menuLines[4] = "|4.) Exit application.............|";
            menuLines[5] = "What do you want to do today? (Enter a number 1-4 and hit ENTER)";
            menuLines[6] = "What do you want to do today? (Enter a number 1 or 2 and hit Enter)";
            menuLines[7] = "|2.) Exit application.............|";

            if (num == 1)
            {
                for (int i = 0; i < 2; i++)
                {
                    Console.WriteLine(menuLines[i]);
                }
                Console.WriteLine(menuLines[7]);
            }
            else
            {
                for (int i = 0; i < 6; i++)
                {
                    Console.WriteLine(menuLines[i]);
                }
            }
        }


        public static bool loggedIn(string userName, string pWord)
        {
         // Description: returns boolean value restricting or allowing certain events
            if (userName == "" || pWord == "")
            { return false; }
            else { return true; }
        }


        public static void credentials()
        {
         // Stores password and username values
            Console.WriteLine("Enter email address:");
            address = Console.ReadLine();
            Console.WriteLine("Enter password:");
            password = Console.ReadLine();
        }


        public static void checkMessages()
        {
         // Accesses gmail class to check messages. Prints string array entries.
            string[] emails = new string[1];
            if (loggedIn(address, password) == true)
            {
                emails = Gmail.getMail(address, password);
                for (int i = 0; i < emails.Length; i++)
                {
                    Console.WriteLine(emails[i]);
                }
            }
            else
            {
                Console.WriteLine("Log in first!");
            }

        }


        public static void sendMessage()
        {
         // Accesses gmail class and sends message.
            if (loggedIn(address, password) == true)
            {
                string sendTo;
                string subject;
                string message;
                Console.WriteLine("Who do you want to send this to? (enter an email address):");
                sendTo = Console.ReadLine();
                Console.WriteLine("What's it about? (enter the subject):");
                subject = Console.ReadLine();
                Console.WriteLine("What's the message? (type the actual message):");
                message = Console.ReadLine();

                Gmail.sendMail(address, password, sendTo, subject, message);
                Console.WriteLine("Message Sent!");
            }
            else
            {
                Console.WriteLine("Log in first!");
            }
        }
    }
}
