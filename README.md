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

Sử dụng Advanced REST Client lấy token:

<img src=http://i.imgur.com/7Dvl3Fs.png width="60%" height="60%" border="1">

1. URL( ô số 1) gồm có địa chỉ của controller, port keystone service và API version 2.0
2. Yêu cầu sử dụng giao thức POST( ô số 2)
3. Chèn data gồm có username, password, tenant name
```sh
{
    "auth": {
        "tenantName": "admin",
        "passwordCredentials": {
            "username": "admin",
            "password": "password123"
        }
    }
}
```
4. Thiết lập Set "Content-Type" header
5. Gửi yêu cầu

Phản hồi về 400 hoặc 401 HTTP có nghĩa là request sai URL hoặc data sai định dạng, phản hồi 200 HTTP là xác thực thành công và trả về file json chứa các thông tin các service của dịch vụ và token của user admin

<img src=http://i.imgur.com/iyv7zjJ.png width="60%" height="60%" border="1">

Ta sẽ lấy token này để xác thực khi sử dụng các dịch vụ khác với các service khác trong OpenStack

###Bước 2: Tương tác với các Indentyfy API trong OpenStack


