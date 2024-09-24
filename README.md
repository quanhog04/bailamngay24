# bailamngay24
using System;

public class SinhVien { public string HoTen { get; set; } public string MSSV { get; set; } public double DiemTrungBinh { get; set; }

// Phuong thuc nhap thong tin sinh vien
public void NhapThongTin()
{
    Console.Write("Nhap ho va ten sinh vien: ");
    HoTen = Console.ReadLine();

    Console.Write("Nhap ma so sinh vien: ");
    MSSV = Console.ReadLine();

    Console.Write("Nhap diem trung binh: ");
    DiemTrungBinh = double.Parse(Console.ReadLine());
}

// Phuong thuc hien thi thong tin sinh vien
public void HienThiThongTin()
{
    Console.WriteLine($"Ho ten: {HoTen}, MSSV: {MSSV}, Diem trung binh: {DiemTrungBinh}");
}
} public class DanhSachSinhVien { private List danhSach; // Danh sach sinh vien

public DanhSachSinhVien()
{
    danhSach = new List<SinhVien>();
}

// Phuong thuc them sinh vien vao danh sach
public void ThemSinhVien(SinhVien sv)
{
    danhSach.Add(sv);
}

// Phuong thuc hien thi danh sach sinh vien
public void HienThiDanhSach()
{
    foreach (var sv in danhSach)
    {
        sv.HienThiThongTin();
    }
}

// Phuong thuc tim sinh vien theo MSSV
public SinhVien TimSinhVienTheoMSSV(string mssv)
{
    foreach (var sv in danhSach)
    {
        if (sv.MSSV == mssv)
        {
            return sv;
        }
    }
    return null; // Khong tim thay sinh vien
}

// Phuong thuc tinh sinh vien co diem trung binh cao nhat
public SinhVien TinhDiemTrungBinhCaoNhat()
{
    if (danhSach.Count == 0)
        return null;

    SinhVien svMax = danhSach[0];
    foreach (var sv in danhSach)
    {
        if (sv.DiemTrungBinh > svMax.DiemTrungBinh)
        {
            svMax = sv;
        }
    }
    return svMax;
}
} class Program { static void Main(string[] args) { DanhSachSinhVien dsSinhVien = new DanhSachSinhVien();

    // Nhap it nhat 3 sinh vien
    for (int i = 0; i < 3; i++)
    {
        SinhVien sv = new SinhVien();
        sv.NhapThongTin();
        dsSinhVien.ThemSinhVien(sv);
    }

    // Hien thi danh sach sinh vien
    Console.WriteLine("\nDanh sach sinh vien:");
    dsSinhVien.HienThiDanhSach();

    // Tim sinh vien co diem trung binh cao nhat
    SinhVien svMax = dsSinhVien.TinhDiemTrungBinhCaoNhat();
    if (svMax != null)
    {
        Console.WriteLine("\nSinh vien co diem trung binh cao nhat:");
        svMax.HienThiThongTin();
    }

    // Tim kiem sinh vien theo MSSV
    Console.Write("\nNhap MSSV de tim kiem sinh vien: ");
    string mssv = Console.ReadLine();
    SinhVien svTimKiem = dsSinhVien.TimSinhVienTheoMSSV(mssv);
    if (svTimKiem != null)
    {
        Console.WriteLine("\nThong tin sinh vien duoc tim thay:");
        svTimKiem.HienThiThongTin();
    }
    else
    {
        Console.WriteLine("Khong tim thay sinh vien voi MSSV nay.");
    }
}
}
