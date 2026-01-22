# Ubuntu Server Homelab 📦

Este repositório contém a configuração completa da minha infraestrutura doméstica rodando sobre o **Ubuntu Server**. O objetivo principal foi centralizar serviços de mídia, nuvem privada e segurança de rede utilizando **Docker** para garantir isolamento e portabilidade.

## 🛠️ Stack Tecnológica

* **SO:** Ubuntu Server 22.04 LTS
* **Orquestração:** Docker & Docker Compose
* **Gestão:** Portainer
* **Rede:** Tailscale (Zero Trust VPN) e Pi-hole (DNS Sinkhole)

---

## 🏗️ Estrutura de Serviços

A infraestrutura foi dividida em "stacks" lógicas para facilitar a manutenção:

### 1. Automação de Mídia e Streaming
Implementação da "Stack ARR" para automatizar todo o fluxo de download e organização de bibliotecas:
* **Jellyfin:** Servidor de streaming local.
* **Sonarr / Radarr / Prowlarr:** Automação de séries, filmes e indexadores.
* **qBittorrent:** Cliente de download integrado à rede.
* **Bazarr:** Gerenciamento automático de legendas.

### 2. Nuvem Privada e Arquivos
* **Nextcloud:** Alternativa ao Google Drive/Dropbox para sincronização de arquivos e fotos.
* **MariaDB:** Banco de dados dedicado para a performance do Nextcloud.
* **Samba (SMB):** Compartilhamento de rede local para acesso rápido via Windows Explorer.

### 3. Observabilidade e Saúde do Sistema
Para monitorar o hardware e a disponibilidade dos containers, utilizo:
* **Prometheus & Node Exporter:** Coleta de métricas de CPU, RAM e I/O de disco.
* **cAdvisor:** Métricas específicas de consumo por container.
* **Grafana:** Visualização de dados (dashboards customizados).
* **Uptime Kuma:** Monitoramento de status e alertas de serviço.

---

## 💾 Gestão de Armazenamento

Um dos pontos principais foi a organização dos volumes. Utilizo um SSD para o sistema e um **HD de 1TB** montado em `/backup` para os dados pesados:
* As configurações (`/config`) ficam no SSD para maior velocidade de leitura.
* Arquivos de mídia, dados do Nextcloud e downloads ficam no HD para aproveitar o espaço.

## 🔒 Acesso Remoto e Segurança

Toda a gestão remota é feita via **Tailscale**. Isso me permite acessar o terminal via SSH ou as interfaces web (Portainer, Grafana) de qualquer lugar sem precisar abrir portas no roteador, mantendo a superfície de ataque nula para a rede externa.

---

1. Clone o repositório: 
   ```bash
   git clone [https://github.com/vinimartinsufrr/ubuntuserver_homelab.git](https://github.com/vinimartinsufrr/ubuntuserver_homelab.git)
  
2. Certifique-se de que os pontos de montagem em `/backup` existem no host.
   ```bash
   docker-compose up -d
   
3. Suba a stack:

4. Acesse o Grafana em `http://<IP-DO-SERVIDOR>:3000` para validar as métricas.
