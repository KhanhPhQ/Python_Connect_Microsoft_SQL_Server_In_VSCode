# Python_Connect_Microsoft_SQL_Server_On_VSCode
Kết nối Microsoft SQL Server trên VSCode

# Tạo User Login Microsoft SQL Server
- Khởi động Microsoft SQL Server
- Tại **Authentication** > Chọn **Windows Authentication** > Connect

![image](https://github.com/user-attachments/assets/0b1e9f4b-2df5-44ea-b41b-484062e7e605)

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

