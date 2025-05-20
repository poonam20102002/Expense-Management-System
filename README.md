## Expense Management System in C#.NET and SQL Server
### Description:
This repository contains a complete Expense Management System developed as a desktop application using C#.NET and SQL Server. The project includes:

- Full source code for seamless integration and customization.
- 15+ dynamically connected Windows Forms for managing expenses efficiently.
- Features such as user authentication, category-wise tracking, and detailed reporting.
- Ideal for students, developers, or businesses looking for a comprehensive solution to track and manage expenses.


## 📖 Overview
The **Expense Management System** is a desktop application built using **C#.NET** and **SQL Server**. It helps users efficiently track and manage their expenses, ensuring better financial planning. This project is designed for personal use or small businesses to monitor transactions and generate expense reports.

---

## 🎯 Features
- User authentication and role-based access (Admin/User).
- Add, edit, delete, and view expenses.
- Categorize expenses for better organization.
- Generate reports for monthly/yearly expenses.
- Data stored securely in an SQL Server database.
- Fully customizable with source code included.

---
💻 Technologies Used
- C#.NET: Backend logic and UI development.
- SQL Server: Database management.
- Crystal Reports: For generating reports.
- Guna UI: Modern UI components.


## 🖼️ Screenshots

* Login Page
  ![1Loginpage](https://github.com/user-attachments/assets/da99845f-f80d-40ce-855a-f23f35288968)

* SignUp Page
  ![2signup](https://github.com/user-attachments/assets/573b423b-8372-4bdb-9412-13232ce6ae3d)


* Dashboard
  ![3Dashboard](https://github.com/user-attachments/assets/f72b1283-b03a-4681-93ef-15ee5e5f4317)

* Category
![4category](https://github.com/user-attachments/assets/48efbfe5-0e96-49a6-ae9e-286376ef370e)

  
* Income

  ![5income](https://github.com/user-attachments/assets/a8bae480-5f95-4d50-b494-9a1b64ed9eb9)


* Expense
![6expense](https://github.com/user-attachments/assets/f7ed847c-e3bd-4c24-a1a9-932583453ede)

  
---

## ⚙️ Prerequisites
- Visual Studio (2019 or later)
- SQL Server (2017 or later)
- .NET Framework (4.7.2 or later)

---

🤝 Contribution
Contributions are welcome! Please follow these steps:

- 1 Fork the repository.
- 2 Create a new branch: git checkout -b feature-name.
- 3 Commit your changes: git commit -m 'Add new feature'.
- 4 Push to the branch: git push origin feature-name.
- 5 Open a pull request.



## 🗄️ Database Setup

Follow these steps to set up the SQL Server database:

1. Open SQL Server Management Studio (SSMS).
2. Create a new database named `ExpenseManagementSystemDB` .
3. Execute the  script to populate the database with sample data.

### SQL Scripts
-- Database: ExpenseManagementSystem
```sql
CREATE DATABASE ExpenseManagementSystem;

USE ExpenseManagementSystem;

-- Create Users Table
CREATE TABLE Users (
    UserID INT IDENTITY(1,1) PRIMARY KEY,
    Username NVARCHAR(50) NOT NULL,
    Password NVARCHAR(255) NOT NULL,
    Role NVARCHAR(20) NOT NULL
);

Create table tblUsers
(
Id int primary key identity(1,1),
username varchar(50),
password varchar(50),
date_create date
)
go


Create table tblCategories
(
id int primary key identity(1,1),
category varchar(200),
type varchar(200),
status varchar(200),
date_insert date
)


Create table tblIncome
(
id int primary key identity(1,1),
category varchar(200),
item varchar(200),
income float,
description nvarchar(500),
date_income date,
date_insert date
)


Create table tblExpenses
(
id int primary key identity(1,1),
category varchar(200),
item varchar(200),
expense float,
description nvarchar(500),
date_expense date,
date_insert date
)

```
## Login Form Code

Below is a sample login form code in C#:

```csharp
// C# Code for a Login Form
using System.Data;
using System.Data.SqlClient;

namespace ExpenseManagementSystemsVBDotNet
{
    public partial class Form1 : Form
    {
        SqlConnection con = new SqlConnection(@"Data Source=DESKTOP-I69OQPV\SQLEXPRESS; Initial Catalog=ExpenseManagementSystemDB;Integrated Security=True");

        public Form1()
        {
            InitializeComponent();
        }
        public static string username;
        public bool checkConnection()
        {
            return (con.State == ConnectionState.Closed) ? true : false;
        }

        private void picExit_Click(object sender, EventArgs e)
        {
            if (MessageBox.Show("Are you sure you want to exit?", "Confirmation Message", MessageBoxButtons.YesNo, MessageBoxIcon.Question) == DialogResult.Yes)
            {
                Application.Exit();
            }
        }

        private void btnSignup_Click(object sender, EventArgs e)
        {
            RegisterForm registerfrm = new RegisterForm();
            registerfrm.Show();
            this.Hide();
        }

        private void chkShowPassword_CheckedChanged(object sender, EventArgs e)
        {
            bool isChecked = chkShowPassword.Checked;
            txtPassword.UseSystemPasswordChar = !isChecked;
        }

        private void btnLogin_Click(object sender, EventArgs e)
        {
            try { 
                if(txtUsername.Text=="" || txtPassword.Text=="")
                {
                    MessageBox.Show("invalid username and password", "Error Message", MessageBoxButtons.OK, MessageBoxIcon.Error);
                }
                else
                {
                    con.Open();
                    string qr = "select username, password from tblUsers where username =@user and password=@pass";
                    using (SqlCommand cmd=new SqlCommand(qr,con))
                    {
                        cmd.Parameters.AddWithValue("@user",txtUsername.Text.Trim());
                        cmd.Parameters.AddWithValue("@pass",txtPassword.Text.Trim());
                        SqlDataAdapter da = new SqlDataAdapter(cmd);
                        DataTable dt = new DataTable();
                        da.Fill(dt);
                        if(dt.Rows.Count>0)
                        {
                            username = txtUsername.Text;
                            //MessageBox.Show("Login Successfully", "Success Message", MessageBoxButtons.OK, MessageBoxIcon.Information);
                            DashboardForm dfrm = new DashboardForm();
                            dfrm.Show();
                            this.Hide();
                        }
                        else
                        {
                            MessageBox.Show("incorrect username/password", "Error Message", MessageBoxButtons.OK, MessageBoxIcon.Error);
                            
                        }
;
                    }
                }
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message);               
            }
            finally
            {
                con.Close();
            }
        }
    }
}



```

## 📺 Video Tutorial

You can watch the **full video tutorial** for this project on my YouTube channel:  
👉 [CoderBaba](https://www.youtube.com/@CoderBaba)

Don't forget to **like**, **share**, and **subscribe** to support me and stay updated with more projects and tutorials! 💖

Happy Coding!





