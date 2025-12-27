
```bash
# List devices
iwctl device list
# Scan for networks
iwctl station wlan0 scan
# List networks
iwctl station wlan0 get-networks
# Connect with password
iwctl --passphrase=YourPassword station wlan0 connect "MyWiFi"

# Vào iwd không cần gõ iwctl phía trước
iwctl
exit
```

```bash
# Chuyển mặc định về chế độ dòng lệnh (Multi-user target)
sudo systemctl set-default multi-user.target
reboot

# Dùng lại tạm thời GUI
sudo systemctl start [sddm|gdm|lightdm]

# Chuyền mặc định về GUI
sudo systemctl set-default graphical.target default.target
```

#### How to use PM2
1. Tạo file cấu hình
Nó sẽ tạo ra file `ecosystem.config.js`
```bash
pm2 init
```
2. Sửa file `ecosystem.config.js`
```js
module.exports = {
  apps : [{
    name   : "x-clone-backend",
    script : "./dist/index.js",
    env: {
      NODE_ENV: "production",
      PORT: 4000
    }
  }]
}
```
3. Chạy bằng file này
```bash
pm2 start ecosystem.config.js
```
3. Các lệnh quản lý thường dùng
```bash
# Chạy dự án đã build
pm2 start dist/index.js --name "x-clone-backend"
# Xem đã chạy hay chưa
pm2 list
# Lưu tiến trình hiện tại
pm2 save
# Tạo script khởi động cùng hệ điều hành
# Nó sẽ tự sinh ra sudo env PATH=... copy và chạy nó
pm2 startup
# Tắt tự động khởi động
pm2 unstartup systemd
# Xem log lỗi (Debug)
pm2 logs x-clone-backend
# Khởi động lại (Sau khi bạn `git pull` code mới và `npm run build` lại)
pm2 restart x-clone-backend
# Dừng server
pm2 stop x-clone-backend
# Theo dõi RAM/CPU
pm2 monit
```

#### Cấu hình tự động tắt backlight ở chế độ CLI
1. Mở file cấu hình GRUB
```bash
sudo nano /etc/default/grub
```
2. Tìm dòng `GRUB_CMDLINE_LINUX_DEFAULT`
3. Thêm tham số `consoleblank=60` vào trong dấu ngoặc kép.
```bash
GRUB_CMDLINE_LINUX_DEFAULT="quiet loglevel=3 consoleblank=60"
```
4. Lưu lại và cập nhật GRUB.
- `Ctrl+X` -> `Y` -> `Enter`.
- Cập nhật GRUB: `sudo grub-mkconfig -o /boot/grub/grub.cfg`
4. Khởi động lại máy: `reboot`. Từ giờ, cứ sau 60 giây không gõ phím, màn hình sẽ tắt ngóm. Muốn dùng lại chỉ cần gõ phím bất kỳ.

#### Sử dụng tmux
1. **Cài đặt:**
```bash
sudo pacman -S tmux
```
2. **Bắt đầu:** Gõ lệnh `tmux`. Bạn sẽ vào một màn hình xanh lá cây ở dưới cùng.
3. **Các phím tắt cơ bản (Phải thuộc lòng):** Tất cả lệnh `tmux` đều bắt đầu bằng phím kích hoạt **`Ctrl` + `b`**, sau đó buông tay ra và bấm phím lệnh:
    - **Chia đôi màn hình dọc:** `Ctrl` + `b`, sau đó bấm `%` (Shift + 5).
    - **Chia đôi màn hình ngang:** `Ctrl` + `b`, sau đó bấm `"` (Shift + ' ).
    - **Di chuyển giữa các ô:** `Ctrl` + `b`, sau đó bấm phím mũi tên ⬅️ ➡️ ⬆️ ⬇️.
    - **Tạo tab mới (Window):** `Ctrl` + `b`, sau đó bấm `c` (create).
    - **Chuyển tab:** `Ctrl` + `b`, sau đó bấm `n` (next) hoặc `p` (previous).
    - **Thoát tạm thời (Detach):** `Ctrl` + `b`, sau đó bấm `d`. (Server vẫn chạy ngầm).
4. **Quay lại phiên làm việc cũ:**
```bash
tmux attach
```
