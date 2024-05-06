# -
최고성능의 가상컴퓨터 만들기
# VirtualBox를 사용하여 Ubuntu 가상 뻬신을 만드는 스크립트 예시입니다.

# 가상 머신 생성
VBoxManage createvm --name "UbuntuVM" --ostype Ubuntu_2560 --register

# 메모리와 CPU 설정
VBoxManage modifyvm "UbuntuVM" --memory 409600 --cpus 20

# 가상 하드 드라이브 생성 및 할당
VBoxManage createhd --filename "~/VirtualBox VMs/UbuntuVM/UbuntuVM.vdi" --size 2000000
VBoxManage storagectl "UbuntuVM" --name "SATA Controller" --add sata --controller IntelAhci
VBoxManage storageattach "UbuntuVM" --storagectl "SATA Controller" --port 0 --device 0 --type hdd --medium "~/VirtualBox VMs/UbuntuVM/UbuntuVM.vdi"

# 네트워크 설정
VBoxManage modifyvm "UbuntuVM" --nic1 nat

# ISO 이미지를 가상 CD/DVD 드라이브에 삽입
VBoxManage storagectl "UbuntuVM" --name "IDE Controller" --add ide
VBoxManage storageattach "UbuntuVM" --storagectl "IDE Controller" --port 0 --device 0 --type dvddrive --medium "/path/to/ubuntu.iso"

# 가상 머신 시작
VBoxManage startvm "UbuntuVM"
