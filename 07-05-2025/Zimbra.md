# Zimbra là gì?
## Zimbra là một email server tích hợp web client, hỗ trợ đầy đủ các dịch vụ như:
- SMTP, POP3, IMAP để gửi/nhận mail
- Webmail truy cập qua trình duyệt
- Lịch làm việc (calendar)
- Danh bạ (contacts)
- Chia sẻ tệp (file sharing)
- Tính năng chat (Zimbra Talk - tùy bản)
## Zimbra có 2 phiên bản:
- Zimbra Open Source Edition (miễn phí)
- Zimbra Network Edition (trả phí – hỗ trợ kỹ thuật, tích hợp nâng cao, backup,...)

# Kiến trúc của Zimbra
- Zimbra là một hệ thống multi-server gồm nhiều thành phần hoạt động cùng nhau:
- MTA (Mail Transfer Agent):	Sử dụng Postfix để gửi/nhận mail.
- LDAP (Lightweight Directory Access Protocol):	Dùng để xác thực và lưu thông tin người dùng
- Mailbox Server:	Chứa hộp thư, webmail và dịch vụ IMAP/POP3
- MTA Proxy, Web Proxy:	Điều phối kết nối từ client
- Antivirus / Antispam:	Dùng ClamAV, Amavis, SpamAssassin để quét virus và lọc spam
