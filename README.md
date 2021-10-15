# ASCIS2021-KhoiDong

B0Ss703@UIT.JustChillOut

# 1. Callmemaybe
<img width="480" alt="Screen Shot 2021-10-10 at 21 03 46" src="https://user-images.githubusercontent.com/64759503/137525681-a8cdcb16-de93-43b0-bcf3-7b3c22e2e904.png">

ciphertext: 1209-852 1209-852 1209-852 1209-852 1477-770 1209-852 1209-852 1209-852 1209-852 1336-941 1336-697 1477-770 1477-770 1477-697 1336-941 1477-697 1477-770 1336-852 1477-697 1477-697 1477-697

Bài này nhìn vào dãy ciphertext thì chúng chỉ có những con số nhất định search tìm hiểu thì đó là mã DTMF

<img width="784" alt="Screen Shot 2021-10-15 at 23 58 30" src="https://user-images.githubusercontent.com/64759503/137525098-88bd0836-4f5e-4f42-a064-f6782ffcd128.png">

Decode ta được dãy số sau: 777767777026630368333

Đến đây thì mình nộp flag luôn không suy nghĩ gì =)))) nhưng tất nhiên là sai rồi làm gì dễ ăn vậy. Đọc lại đề bài thì nó có nhắc tới một cuộc gọi thì có lẽ liên quan tới số điện thoại.

Và đúng như vậy dãy số này chính là Phone Keypad Cipher dễ hiểu hơn chính là type text trên cái điện thoại bàn phím số ngày trước
![zt8iw3vg87131](https://user-images.githubusercontent.com/64759503/137526452-e37416b6-4de3-4679-a7ac-06e5ed026a94.jpeg)

Dựa vào bàn phím huyền thoại đó sẽ ra được: SMS AND DMTF

```FLAG{SMS AND DMTF}```

# 2. Calculate me

<img width="488" alt="Screen Shot 2021-10-10 at 21 04 07" src="https://user-images.githubusercontent.com/64759503/137530169-f1386cce-ea02-4d81-a9f7-9a9afb6d747d.png">


Một bài programming cơ bản
```py 
import socket
import re
import cv2


IP, PORT = ('125.235.240.166', 20103)


def receive_one_line(s):
    r = b''
    while (True):
        t = s.recv(1)
        if t == b'\n': break
        r = r + t
    return r.decode()

def send_one_line(s, data):
    data = str(data)
    s.send((data + '\n').encode())

def main():
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.connect((IP, PORT))
    banner = receive_one_line(s)
    print(banner)
    banner = receive_one_line(s)
    print(banner)
    for i in range(1000):
        banner = receive_one_line(s)
        print(banner)
        a=re.findall(r'\d+', banner)
        print(a)
        n=len(a[0])
        print(len(a[0]))
        print(len(a))
        x=banner[len(a[0])]
        
        print(x)
        if x=="+":
            result=int(a[0])+int(a[1])
       
        elif x=="*":
            result=int(a[0])*int(a[1])
         
        elif x=="/":
            result=int(int(a[0])/int(a[1]))
          
        elif x=="-": 
            result=int(a[0])-int(a[1])
           
        print(result)
        s.send((str(result) + '\n').encode())
        banner = receive_one_line(s)
        print(banner)
    
        banner = receive_one_line(s)
        print(banner)
        
if __name__ == '__main__':
    main()
```
<img width="498" alt="Screen Shot 2021-10-09 at 11 12 07" src="https://user-images.githubusercontent.com/64759503/137530102-0cc76363-22a5-41a1-bfd5-b36a50b27e67.png">

Xin lỗi mọi người vì cái code củ chuối này nhưng ra flag là được =))))

```ASCIS{3v3ry0n3_sh0uld_kn0w_pr0gramm1ng}```

# 3. Simple For

<img width="489" alt="Screen Shot 2021-10-10 at 21 04 01" src="https://user-images.githubusercontent.com/64759503/137530752-6ce13b7f-31a9-4e6a-9c00-fb56e6d51005.png">


Bài này cũng đơn giản. Dùng wireshark mò mò chút là ra rồi 

<img width="963" alt="Screen Shot 2021-10-16 at 00 56 20" src="https://user-images.githubusercontent.com/64759503/137531930-fb2a2196-04e8-4f05-bad0-7d9c6bdf8432.png">

Save file flag về thôi =))))

```ASCIS{n3tw0rk_f0r3ns1c_1s_n0t_h4rd}```








