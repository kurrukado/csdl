CREATE DATABASE QuanLyHocTap;
GO

USE QuanLyHocTap;
GO

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

    FOREIGN KEY(MaQT)
        REFERENCES QuocTich(MaQT),

    FOREIGN KEY(MaDT)
        REFERENCES DanToc(MaDT),

    FOREIGN KEY(MaTG)
        REFERENCES TonGiao(MaTG),

    FOREIGN KEY(MaXa)
        REFERENCES XaPhuong(MaXa),

    FOREIGN KEY(MaTinh)
        REFERENCES TinhThanh(MaTinh)
);

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

    FOREIGN KEY(MaTinh)
        REFERENCES TinhThanh(MaTinh)
);

CREATE TABLE MonHoc
(
    MaMH CHAR(5) PRIMARY KEY,
    TenMH NVARCHAR(100),
    SoTinChi INT
);

CREATE TABLE HocKy
(
    MaHK CHAR(4) PRIMARY KEY,
    TenHocKy NVARCHAR(50),
    NamHoc VARCHAR(9)
);

CREATE TABLE DangKyHoc
(
    MaDK INT IDENTITY(1,1) PRIMARY KEY,
    MaSV CHAR(6),
    MaMH CHAR(5),
    MaHK CHAR(4),

    FOREIGN KEY(MaSV) REFERENCES SinhVien(MaSV),
    FOREIGN KEY(MaMH) REFERENCES MonHoc(MaMH),
    FOREIGN KEY(MaHK) REFERENCES HocKy(MaHK)
);

CREATE TABLE DiemThi
(
    MaDK INT PRIMARY KEY,

    DiemA1 DECIMAL(4,2),
    DiemA2 DECIMAL(4,2),
    DiemA3 DECIMAL(4,2),

    FOREIGN KEY(MaDK) REFERENCES DangKyHoc(MaDK)
);

INSERT INTO MonHoc VALUES
('MH001',N'Cơ sở dữ liệu',3),
('MH002',N'Lập trình C#',3),
('MH003',N'Cấu trúc dữ liệu',3),
('MH004',N'Mạng máy tính',3),
('MH005',N'Hệ điều hành',3);

INSERT INTO HocKy VALUES
('HK01',N'Học kỳ 1','2025-2026'),
('HK02',N'Học kỳ 2','2025-2026');

INSERT INTO SinhVien VALUES
('240001',N'Nguyễn Văn An','2005-01-15',N'Nam',N'Khánh Hòa',N'Nha Trang',N'Việt Nam',N'Kinh',N'Không',N'Nha Trang','2020-09-15',NULL,N'Nha Trang',N'Vĩnh Hải',N'Khánh Hòa',N'Bình Dương'),

('240002',N'Trần Thị Bình','2005-03-20',N'Nữ',N'Đà Nẵng',N'Đà Nẵng',N'Việt Nam',N'Kinh',N'Không',N'Đà Nẵng','2020-09-15',NULL,N'Đà Nẵng',N'Hải Châu',N'Đà Nẵng',N'Bình Dương'),

('240003',N'Lê Quốc Cường','2005-07-11',N'Nam',N'Hà Nội',N'Hà Nội',N'Việt Nam',N'Kinh',N'Không',N'Hà Nội','2020-09-15',NULL,N'Hà Nội',N'Cầu Giấy',N'Hà Nội',N'Bình Dương'),

('240004',N'Phạm Minh Đức','2005-05-06',N'Nam',N'Hải Phòng',N'Hải Phòng',N'Việt Nam',N'Kinh',N'Không',N'Hải Phòng','2020-09-15',NULL,N'Hải Phòng',N'Ngô Quyền',N'Hải Phòng',N'Bình Dương'),

('240005',N'Hoàng Gia Hân','2005-04-01',N'Nữ',N'Cần Thơ',N'Cần Thơ',N'Việt Nam',N'Kinh',N'Không',N'Cần Thơ','2020-09-15',NULL,N'Cần Thơ',N'Ninh Kiều',N'Cần Thơ',N'Bình Dương'),

('240006',N'Ngô Thành Long','2005-08-22',N'Nam',N'Đồng Nai',N'Biên Hòa',N'Việt Nam',N'Kinh',N'Không',N'Biên Hòa','2020-09-15',NULL,N'Đồng Nai',N'Tân Hiệp',N'Đồng Nai',N'Bình Dương'),

('240007',N'Võ Thanh Mai','2005-02-28',N'Nữ',N'Bình Định',N'Quy Nhơn',N'Việt Nam',N'Kinh',N'Không',N'Quy Nhơn','2020-09-15',NULL,N'Bình Định',N'Ghềnh Ráng',N'Bình Định',N'Bình Dương'),

('240008',N'Đặng Quốc Nam','2005-09-18',N'Nam',N'Gia Lai',N'Pleiku',N'Việt Nam',N'Kinh',N'Không',N'Pleiku','2020-09-15',NULL,N'Gia Lai',N'Diên Hồng',N'Gia Lai',N'Bình Dương'),

('240009',N'Bùi Hải Yến','2005-06-17',N'Nữ',N'Lâm Đồng',N'Đà Lạt',N'Việt Nam',N'Kinh',N'Không',N'Đà Lạt','2020-09-15',NULL,N'Lâm Đồng',N'Phường 1',N'Lâm Đồng',N'Bình Dương'),

('240010',N'Đỗ Đức Phong','2005-12-10',N'Nam',N'Quảng Nam',N'Tam Kỳ',N'Việt Nam',N'Kinh',N'Không',N'Tam Kỳ','2020-09-15',NULL,N'Quảng Nam',N'An Mỹ',N'Quảng Nam',N'Bình Dương');

INSERT INTO DangKyHoc(MaSV,MaMH,MaHK) VALUES
('240001','MH001','HK01'),
('240001','MH002','HK01'),

('240002','MH001','HK01'),
('240002','MH003','HK01'),

('240003','MH002','HK01'),
('240003','MH004','HK01'),

('240004','MH001','HK01'),
('240004','MH005','HK01'),

('240005','MH003','HK01'),
('240005','MH005','HK01'),

('240006','MH002','HK01'),
('240006','MH003','HK01'),

('240007','MH004','HK01'),
('240007','MH005','HK01'),

('240008','MH001','HK01'),
('240008','MH002','HK01'),

('240009','MH003','HK01'),
('240009','MH004','HK01'),

('240010','MH002','HK01'),
('240010','MH005','HK01');

INSERT INTO DiemThi
SELECT
    MaDK,
    ROUND(RAND(CHECKSUM(NEWID()))*4+6,2),
    ROUND(RAND(CHECKSUM(NEWID()))*4+6,2),
    ROUND(RAND(CHECKSUM(NEWID()))*4+6,2)
FROM DangKyHoc;
