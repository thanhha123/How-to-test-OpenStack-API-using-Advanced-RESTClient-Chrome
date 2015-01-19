# How-to-test-OpenStack-API-using-Advanced-RESTClient-Chrome
## Cài đặt ứng dụng
 Vào web store của chrome, tìm kiếm và cài ứng dụng Advanced RESTClient về cho trình duyệt
 
 
 <img src=http://i.imgur.com/SE9BloY.png width="60%" height="60%" border="1">

Giao diện của ứng dụng như dưới:

<img src=http://i.imgur.com/ACRfcit.png width="60%" height="60%" border="1">


1. Advanced RESTClient hỗ trợ các giao thức GET, POST, PUT, PATCH, DELETE, HEAD
2. Chèn thêm header cho yêu cầu, có thể chèn theo raw hoặc theo form
3. Với các giao thức POST hoặc PUT ta cần thêm data khi gửi yêu cầu, ta thêm data ở ô số 3 này cũng dưới dạng raw hoặc form
4. Các option của ứng dụng

## Sử dụng Advanced RESTClient để test OPENSTACK API

Openstack gồm có Block Storage API, Compute API, Data service API, Compute API, Indentify API, Image Service API, Networking API, Object Storage API,v.v.. Bạn có thể tham khảo tại:

```sh
http://developer.openstack.org/api-ref.html
```

Dưới đây mình sẽ thực hiện sử dụng ứng dụng Advanced REST Client giao tiếp với Indentify API. Cụ thể hơn là lấy tokens(POST request),hiển thị ra danh sách user(GET request),danh dách tenant(GET request)

###Bước 1: Xác thực hệ thống

Khi giao tiếp với bất kỳ thành phần nào trong OpenStack đều cần có xác thực. Để hiển thị lên danh dách các user, danh sách role, danh sách tenant cần có Token admin để xác thực. Để lấy được token này ta sử dụng giao thức POST với API v2.0. Xem mô tả API này tại:
```sh
http://developer.openstack.org/api-ref-identity-v2.html
```
<img src=http://i.imgur.com/ysVBi2V.png width="60%" height="60%" border="1">


