# The table structure is as follows :

<img src="https://user-images.githubusercontent.com/128796172/227575725-47333330-a4e8-47b5-af3f-6526735905ed.png">
<img src="https://user-images.githubusercontent.com/128796172/227575739-5aadce3c-8967-4ef2-bc4a-6a74619ae3a1.png">
<img src="https://user-images.githubusercontent.com/128796172/227575751-e37e2a2e-dec4-47bd-a141-8271b6c5b77d.png">

# Write query language:

`--1.Danh sách mã số, họ tên sinh viên và tên những môn học mà những sinh viên có đăng ký học và có kết quả thi.`

select sinhvien.masv, sinhvien.hosv, sinhvien.tensv, dangky.mamh, monhoc.tenmh, dangky.hocky, ketqua.diemlt, ketqua.diemth, ketqua.lanthi 

from sinhvien

join dangky on (sinhvien.masv = dangky.masv)

join monhoc on (dangky.mamh = monhoc.mamh)

join ketqua on (sinhvien.masv = ketqua.masv)


`--2. Danh sách tên của tất cả các môn học và tên giảng viên phụ trách lý thuyết tương ứng, nếu có.`

select giangvien.hoten,giangday.phutrach, monhoc.tenmh

from monhoc join giangday on monhoc.mamh=giangday.mamh join giangvien on giangday.magv=giangvien.magv
where giangday.phutrach = 'LT'

`--3. Cho biết mã số và họ tên giảng viên không có thân nhân nào.`

select giangvien.magv, giangvien.hoten, thannhan.hotentn

from giangvien left join thannhan on giangvien.magv=thannhan.magv

where thannhan.hotentn IS NULL

`--4. Danh sách những sinh viên và tên những môn học đã đăng ký học nhưng không có kết quả thi của môn học.`

select * --distinct sinhvien.masv,hoten,tensv,tenmh

from ketqua right join sinhvien on ketqua.masv=sinhvien.masv right join dangky on sinhvien.masv=dangky.masv

where ketqua.masv is null

`--5. Danh sách tên của những môn học đã được phân công giảng dạy trong học kỳ 1 năm ‘2014-2015’ nhưng không có sinh viên đăng ký.`

select monhoc.tenmh

from monhoc join giangday on monhoc.mamh = giangday.mamh 

right join dangky on giangday.namhoc = dangky.namhoc

`--6. Tạo danh sách có mã số và họ tên giảng viên dạy lý thuyết môn học tên là ‘Cơ sở dữ liệu’ trong học kỳ 2, 2014-2015.`

select giangvien.magv,giangvien.hoten, giangday.phutrach, monhoc.tenmh, giangday.namhoc, giangday.hocky

from giangvien join giangday on giangvien.magv = giangday.magv join monhoc on giangday.mamh = monhoc.mamh

where giangday.phutrach='LT' and monhoc.tenmh like N'Cơ sở dữ liệu%' and giangday.hocky = 2 and giangday.namhoc = '2014-2015'

`--7. Tạo danh sách có mã số, họ tên các giảng viên và mã môn học mà giảng viên được hoặc không được phân công giảng dạy lý thuyết trong năm 2014-2015`

select giangvien.magv,giangvien.hoten, monhoc.mamh,giangday.phutrach,giangday.namhoc

from giangvien right join giangday on giangvien.magv = giangday.magv right join monhoc on giangday.mamh = monhoc.mamh

where giangday.phutrach = 'LT'and giangday.namhoc = '2014-2015' 
