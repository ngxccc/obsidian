- **Dùng `choco`** để cài đặt các ứng dụng GUI và driver (ví dụ: `choco install vscodium chrome powertoys`).
- **Dùng `scoop`** để cài đặt các công cụ CLI và dev (ví dụ: `scoop install neovim nodejs fd`).
### All my packages
`choco`
- googlechrome
- autohotkey.install
- zalopc
- chrome
- powertoys
- dbeaver
`scoop`
(Bucket: Main)
- chezmoi
- git
- bun
### How to auto run autohotkey script on boot
1. Nhấn phím `Win` + `R` để mở hộp thoại "Run". Sau đó nhập `shell:startup`
2. Tạo shortcut cho file script đó rồi dán vào mục Startup
### Check list
- [ ] chuyển hoá các app,... sang choco, scoop
- [x] tìm tool tạo symlink
- [x] làm sao để chạy file Main.ank khi khởi động windows
- [ ] chuyển .dotfiles-win sang chezmoi
- [x] public obsidian vault lên github
    - có thể dùng private repo
    - nhớ thêm `.gitignore`
    ```txt
    # Bỏ qua cache và workspace của Obsidian
    .obsidian/workspace.json
    .obsidian/workspaces.json
    .obsidian/cache/
    .obsidian/graph.json
    .obsidian/publish.json
    
    # Bỏ qua file rác của hệ thống
    .trash/
    *.log
    Thumbs.db
    .DS_Store
    ```
- [ ] 
