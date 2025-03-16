# [Python] Kết Nối Microsoft SQL Server Trong VSCode
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

# Cài đặt thư viện trên VSCode
```bash
pip install --upgrade pyodbc
```

![image](https://github.com/user-attachments/assets/f1fa2931-836b-45b5-9336-dfb5bd5b9d04)

```bash
import pyodbc

print(pyodbc.drivers())
```
![image](https://github.com/user-attachments/assets/e1a3ff4d-7c73-4825-8cc9-d912c62441cf)

# Tạo kết nối Database và lấy dữ liệu
> Cấu trúc dự án

```bash
Dự_án/
├── config.ini
├── main.py
└── utils/
    └── database_handler.py
```

- config.ini
```bash
[database]
driver = {ODBC Driver 17 for SQL Server}
server = Server Name
database = Database Name
username = User Login
password = Password
```

- main.py
```bash
from utils.database_handler import DatabaseHandler

def main():
    db_handler = DatabaseHandler()
    # Lấy dữ liệu từ Database
    if db_handler.connection:
        get_data = db_handler.connection.cursor()
        get_data.execute("SELECT * FROM dbo.TBL_SYMBOLS")
        print(get_data.fetchone())
        db_handler.close()

if __name__ == "__main__":
    main()
```

- database_handler.py
```bash
import os
import configparser
import pyodbc

class DatabaseHandler:
    def __init__(self, config_file='config.ini'):
        self.config_file = config_file
        self._load_config()
        self.connection = self._connect()
    
    def _load_config(self):        
        # Xác định đường dẫn tuyệt đối đến file config.ini
        config_path = os.path.join(os.path.dirname(__file__), '..', 'config.ini')

        # Tạo đối tượng configparser
        config = configparser.ConfigParser()
        config.read(config_path, encoding='utf-8')

        # Lấy thông tin kết nối từ file cấu hình
        self.driver = config['database']['driver']
        self.server = config['database']['server']
        self.database = config['database']['database']
        self.username = config['database']['username']
        self.password = config['database']['password']

    def _connect(self):
        # Chuỗi kết nối CSDL
        connection_string = f"DRIVER={self.driver};SERVER={self.server};DATABASE={self.database};UID={self.username};PWD={self.password};"

        # Kết nối đến CSDL
        try:
            connection = pyodbc.connect(connection_string)
            print("Kết nối CSLD thành công.")
            return connection
        except Exception as e:
            print(f"Lỗi kết nối CSDL: {e}")
            return None

    def close(self):
        # Đóng kết nối CSDL
        if self.connection:
            self.connection.close()
            print("Đóng kết nối CSDL.")
```

> Chạy File main.py

![image](https://github.com/user-attachments/assets/db1b28a2-1975-435b-9af8-921983b302a8)
