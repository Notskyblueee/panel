#!/usr/bin/env bash

# ========= Colors =========
BLUE='\033[1;34m'
CYAN='\033[1;36m'
WHITE='\033[1;37m'
NC='\033[0m'

clear

while true; do
clear
echo -e "${BLUE}"
echo " ╔═╦╗╔╦╗╔═╦═╦╦╦╦╗╔═╗"
echo " ║╚╣║║║╚╣╚╣╔╣╔╣║╚╣═╣"
echo "  ╠╗║╚╝║║╠╗║╚╣║║║║║═╣"
echo " ╚═╩══╩═╩═╩═╩╝╚╩═╩═╝"
echo -e "${CYAN}Powered By Notskyblueee${NC}"
echo
echo -e "${BLUE}Petrodactyle Installation (IPv6 Ready):${NC}"
echo
echo -e "${CYAN}1.${WHITE} Panel Install (IPv4 / IPv6)"
echo -e "${CYAN}2.${WHITE} Node Install (IPv4 / IPv6)"
echo -e "${CYAN}3.${WHITE} Auto Wings Install"
echo -e "${CYAN}4.${WHITE} Tailscale Install"
echo -e "${CYAN}5.${WHITE} Tailscale Up"
echo -e "${CYAN}6.${WHITE} Cloudflare Tunnel Install"
echo -e "${CYAN}7.${WHITE} Start Wings"
echo -e "${CYAN}8.${WHITE} Restart Wings"
echo -e "${CYAN}9.${WHITE} Stop Wings"
echo -e "${CYAN}10.${WHITE} Exit"
echo
read -p "Choose - 1 to 10 : " choice

case $choice in
1)
    bash <(curl -s https://pterodactyl-installer.se)
    ;;
2)
    bash <(curl -s https://pterodactyl-installer.se)
    ;;
3)
    echo -e "${CYAN}Installing Wings Automatically...${NC}"
    curl -L -o /usr/local/bin/wings https://github.com/pterodactyl/wings/releases/latest/download/wings_linux_amd64
    chmod +x /usr/local/bin/wings
    mkdir -p /etc/pterodactyl
    echo -e "${WHITE}Wings installed. Add config.yml from panel.${NC}"
    ;;
4)
    curl -fsSL https://tailscale.com/install.sh | sh
    ;;
5)
    sudo tailscale up
    ;;
6)
    echo -e "${CYAN}Installing Cloudflare Tunnel...${NC}"
    mkdir -p --mode=0755 /usr/share/keyrings
    curl -fsSL https://pkg.cloudflare.com/cloudflare-main.gpg \
    | tee /usr/share/keyrings/cloudflare-main.gpg >/dev/null

    echo "deb [signed-by=/usr/share/keyrings/cloudflare-main.gpg] https://pkg.cloudflare.com/cloudflared $(lsb_release -cs) main" \
    | tee /etc/apt/sources.list.d/cloudflared.list

    apt update && apt install cloudflared -y
    echo -e "${WHITE}Run: cloudflared tunnel login${NC}"
    ;;
7)
    systemctl start wings
    ;;
8)
    systemctl restart wings
    ;;
9)
    systemctl stop wings
    ;;
10)
    echo -e "${CYAN}Exiting...${NC}"
    exit 0
    ;;
*)
    echo -e "${WHITE}Invalid option! Try again.${NC}"
    sleep 2
    ;;
esac
done
