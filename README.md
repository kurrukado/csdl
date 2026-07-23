```sql
CREATE DATABASE QuanLyHocTap;
GO

USE QuanLyHocTap;
GO

-----------------------------------------------------
-- DANH MỤC
-----------------------------------------------------

CREATE TABLE QuocTich
(
    MaQT INT IDENTITY(1,1) PRIMARY KEY,
    TenQT NVARCHAR(50) NOT NULL
);

CREATE TABLE DanToc
(
    MaDT INT IDENTITY(1,1) PRIMARY KEY,
    TenDT NVARCHAR(50) NOT NULL
);

CREATE TABLE TonGiao
(
    MaTG INT IDENTITY(1,1) PRIMARY KEY,
    TenTG NVARCHAR(50) NOT NULL
);

CREATE TABLE TinhThanh
(
    MaTinh INT IDENTITY(1,1) PRIMARY KEY,
    TenTinh NVARCHAR(100) NOT NULL
);

CREATE TABLE XaPhuong
(
    MaXa INT IDENTITY(1,1) PRIMARY KEY,
    TenXa NVARCHAR(100) NOT NULL,
    MaTinh INT NOT NULL,

    FOREIGN KEY (MaTinh)
        REFERENCES TinhThanh(MaTinh)
);

-----------------------------------------------------
-- SINH VIÊN
-----------------------------------------------------

CREATE TABLE SinhVien
(
    MaSV CHAR(6) PRIMARY KEY,
    HoTen NVARCHAR(100) NOT NULL,
    NgaySinh DATE,
    GioiTinh NVARCHAR(5),

    NoiSinh NVARCHAR(100),
    QueQuan NVARCHAR(100),

    MaQT INT,
    MaDT INT,
    MaTG INT,

    TPXuatThan NVARCHAR(100),

    NgayVaoDoan DATE,
    NgayVaoDang DATE,

    NoiThuongTru NVARCHAR(200),

    MaXa INT,
    MaTinh INT,

    NoiOHienNay NVARCHAR(200),

    FOREIGN KEY (MaQT) REFERENCES QuocTich(MaQT),
    FOREIGN KEY (MaDT) REFERENCES DanToc(MaDT),
    FOREIGN KEY (MaTG) REFERENCES TonGiao(MaTG),
    FOREIGN KEY (MaXa) REFERENCES XaPhuong(MaXa),
    FOREIGN KEY (MaTinh) REFERENCES TinhThanh(MaTinh)
);

-----------------------------------------------------
-- MÔN HỌC
-----------------------------------------------------

CREATE TABLE MonHoc
(
    MaMH CHAR(5) PRIMARY KEY,
    TenMH NVARCHAR(100) NOT NULL,
    SoTinChi INT NOT NULL
);

-----------------------------------------------------
-- HỌC (BẢNG LIÊN KẾT)
-----------------------------------------------------

CREATE TABLE Hoc
(
    MaHoc INT IDENTITY(1,1) PRIMARY KEY,

    MaSV CHAR(6) NOT NULL,
    MaMH CHAR(5) NOT NULL,

    HocKy NVARCHAR(20),
    NamHoc VARCHAR(9),

    DiemA1 DECIMAL(4,2),
    DiemA2 DECIMAL(4,2),
    DiemA3 DECIMAL(4,2),

    FOREIGN KEY (MaSV)
        REFERENCES SinhVien(MaSV),

    FOREIGN KEY (MaMH)
        REFERENCES MonHoc(MaMH)
);
GO

-----------------------------------------------------
-- DỮ LIỆU DANH MỤC
-----------------------------------------------------

INSERT INTO QuocTich(TenQT)
VALUES (N'Việt Nam');

INSERT INTO DanToc(TenDT)
VALUES (N'Kinh');

INSERT INTO TonGiao(TenTG)
VALUES (N'Không');

INSERT INTO TinhThanh(TenTinh)
VALUES
(N'Khánh Hòa'),
(N'Đà Nẵng'),
(N'Hà Nội');

INSERT INTO XaPhuong(TenXa,MaTinh)
VALUES
(N'Vĩnh Hải',1),
(N'Hải Châu',2),
(N'Cầu Giấy',3);

-----------------------------------------------------
-- MÔN HỌC
-----------------------------------------------------

INSERT INTO MonHoc
VALUES
('MH001',N'Cơ sở dữ liệu',3),
('MH002',N'Lập trình C#',3),
('MH003',N'Cấu trúc dữ liệu',3),
('MH004',N'Mạng máy tính',3),
('MH005',N'Hệ điều hành',3);

-----------------------------------------------------
-- SINH VIÊN
-----------------------------------------------------

INSERT INTO SinhVien
VALUES
('240001',N'Nguyễn Văn An','2005-01-15',N'Nam',
N'Khánh Hòa',N'Nha Trang',
1,1,1,
N'Nha Trang',
'2020-09-15',NULL,
N'Nha Trang',
1,1,
N'Bình Dương'),

('240002',N'Trần Thị Bình','2005-03-20',N'Nữ',
N'Đà Nẵng',N'Đà Nẵng',
1,1,1,
N'Đà Nẵng',
'2020-09-15',NULL,
N'Đà Nẵng',
2,2,
N'Bình Dương'),

('240003',N'Lê Quốc Cường','2005-07-11',N'Nam',
N'Hà Nội',N'Hà Nội',
1,1,1,
N'Hà Nội',
'2020-09-15',NULL,
N'Hà Nội',
3,3,
N'Bình Dương');

-----------------------------------------------------
-- HỌC
-----------------------------------------------------

INSERT INTO Hoc
(MaSV,MaMH,HocKy,NamHoc,DiemA1,DiemA2,DiemA3)
VALUES

('240001','MH001',N'HK1','2025-2026',8.5,8.0,9.0),
('240001','MH002',N'HK1','2025-2026',7.5,8.0,8.5),

('240002','MH001',N'HK1','2025-2026',9.0,8.5,9.5),
('240002','MH003',N'HK1','2025-2026',7.0,7.5,8.0),

('240003','MH002',N'HK1','2025-2026',8.0,8.5,9.0),
('240003','MH004',N'HK1','2025-2026',9.5,9.0,8.5);
GO
```
