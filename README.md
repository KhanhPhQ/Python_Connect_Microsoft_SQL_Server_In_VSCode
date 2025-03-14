# Python_Connect_Microsoft_SQL_Server_On_VSCode
Kết nối Microsoft SQL Server trên VSCode

# Tạo User Login Microsoft SQL Server và khởi động lại dịch vụ SQL Server
> Tạo User Login Microsoft SQL Server

- Khởi động Microsoft SQL Server
- Tại **Authentication** > Chọn **Windows Authentication** > Connect

![image](https://github.com/user-attachments/assets/0b1e9f4b-2df5-44ea-b41b-484062e7e605)

- Tại **Object Explorer** > Mở **Server Name** > Mở **Security** > Chuột phải vào **Logins** > Chọn **New Login...**

![image](https://github.com/user-attachments/assets/66adc12e-34e6-4161-a5e9-da8302bbf6fa)

- Tại page **General** > Chọn và nhập trong những khung đỏ

![image](https://github.com/user-attachments/assets/ecb4e5bc-7515-454d-ae67-1e3f764151e8)

- Tại page **Server Roles** > Chọn tất cả các Roles trong khung đỏ

![image](https://github.com/user-attachments/assets/2545cd26-8186-41d2-8750-0a5f655467f5)

- Tại page **Status** > Mục **Login** > Chọn **Enabled**

![image](https://github.com/user-attachments/assets/597e92d6-46a6-43a0-8316-bf59f699a0df)

=> Xong bước tạo User Login SQL

> Khởi động lại dịch vụ SQL Server

- Chọn Start Menu > Tìm kiếm **Configuration Manager** > Chọn **SQL Server 20XX Configuration Manager**

![image](https://github.com/user-attachments/assets/9b945723-26fb-456f-b620-aff7ebe9a166)

- Cửa sổ **SQL Server Configuration Manager** bật lên > Chọn menu **SQL Server Configuration Manager (Local)** > Chọn **SQL Server Services** > Chuột phải vào **SQL Server (MSSQLSERVER)** > Chọn **Restart**

![image](https://github.com/user-attachments/assets/23e4b13b-f30e-4fb9-ab7b-c618632adc22)

=> Chờ xíu để dịch vụ SQL Server khởi động lại.

- Đăng nhập với User Login đã tạo.

![image](https://github.com/user-attachments/assets/7275eff8-8d8d-4b91-894f-c1a05f7a8788)

# Cài đặt thư viện
```bash
pip install --upgrade pyodbc
```

![image](https://github.com/user-attachments/assets/f1fa2931-836b-45b5-9336-dfb5bd5b9d04)

```bash
import pyodbc

print(pyodbc.drivers())
```
![image](https://github.com/user-attachments/assets/e1a3ff4d-7c73-4825-8cc9-d912c62441cf)

