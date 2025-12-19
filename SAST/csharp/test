using System;
using System.Data.SqlClient;
using System.Diagnostics;
using System.IO;
using System.Runtime.Serialization.Formatters.Binary;
using System.Security.Cryptography;
using System.Text;
using Microsoft.AspNetCore.Mvc;

namespace SastTestApp
{
    public class VulnerableExamples : Controller
    {
        // 1. Hardcoded credentials
        private const string DbUser = "admin";
        private const string DbPassword = "P@ssw0rd123";

        // 2. SQL Injection
        public void SqlInjectionExample(string userInput)
        {
            string connectionString =
                "Server=localhost;Database=TestDb;User Id=admin;Password=admin123;";

            string query = "SELECT * FROM Users WHERE Username = '" + userInput + "'";

            using (SqlConnection conn = new SqlConnection(connectionString))
            {
                SqlCommand cmd = new SqlCommand(query, conn);
                conn.Open();
                cmd.ExecuteReader();
            }
        }

        // 3. Command Injection
        public void CommandInjectionExample(string fileName)
        {
            Process.Start("cmd.exe", "/c dir " + fileName);
        }

        // 4. Path Traversal
        public string PathTraversalExample(string file)
        {
            string path = "C:\\AppData\\Files\\" + file;
            return System.IO.File.ReadAllText(path);
        }

        // 5. Insecure Deserialization
        public object InsecureDeserializationExample(byte[] data)
        {
            BinaryFormatter formatter = new BinaryFormatter();
            using (MemoryStream ms = new MemoryStream(data))
            {
                return formatter.Deserialize(ms);
            }
        }

        // 6. Weak Cryptography (MD5)
        public string WeakHashExample(string input)
        {
            MD5 md5 = MD5.Create();
            byte[] hash = md5.ComputeHash(Encoding.UTF8.GetBytes(input));
            return Convert.ToBase64String(hash);
        }

        // 7. Cross-Site Scripting (XSS)
        [HttpGet]
        public IActionResult XssExample(string comment)
        {
            return Content("<html><body>User comment: " + comment + "</body></html>", "text/html");
        }

        // 8. Missing Authorization Check
        public void DeleteUser(int userId)
        {
            // No authentication or authorization check
            Console.WriteLine("User deleted: " + userId);
        }
    }
}
