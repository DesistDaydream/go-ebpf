https://ebpf-go.dev/guides/getting-started/

需要安装如下依赖

- Linux Kernel 版本 >= 5.7, 支持 bpf_link
- apt install clang
- apt install llvm
- apt install libbpf-dev
- ln -sf /usr/include/asm-generic/ /usr/include/asm
  - 因为示例期望找到 `<asm/types.h>`

初始化项目

```bash
go mod init github.com/DesistDaydream/go-ebpf
go mod tidy
```

创建 counter.c 和 gen.go 文件，执行如下命令

```bash
go get github.com/cilium/ebpf/cmd/bpf2go
go generate
```

命令输出内容:

```bash
Compiled /mnt/d/projects/DesistDaydream/go-ebpf/counter_bpfel.o
Stripped /mnt/d/projects/DesistDaydream/go-ebpf/counter_bpfel.o
Wrote /mnt/d/projects/DesistDaydream/go-ebpf/counter_bpfel.go
Compiled /mnt/d/projects/DesistDaydream/go-ebpf/counter_bpfeb.o
Stripped /mnt/d/projects/DesistDaydream/go-ebpf/counter_bpfeb.o
Wrote /mnt/d/projects/DesistDaydream/go-ebpf/counter_bpfeb.go
```

这会生成如下几个文件

- counter_bpfeb.go
- counter_bpfeb.o
- counter_bpfel.go
- counter_bpfel.o

创建 main.go 文件并执行如下命令

```bash
go build -o bin/go-ebpf
```

运行 go-ebpf 程序即可

TODO:

- 为什么不可以直接 go run *.go ?
- 如何将这些文件放到其他目录而不是项目根目录