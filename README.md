Guia Completo: Configurando e Utilizando o WSL2 + Docker no Windows
Este guia fornece instruções detalhadas sobre como configurar o WSL2 (Windows Subsystem for Linux, versão 2) e o Docker no Windows, permitindo que você crie um ambiente de desenvolvimento robusto.

Preparação
Antes de começar, certifique-se de que o WSL2 está instalado e configurado em sua máquina Windows. Se ainda não o fez, você pode seguir as instruções da documentação oficial da Microsoft.

Instalando o Docker no WSL2
A instalação do Docker no WSL2 é semelhante à instalação em qualquer distribuição Linux. Aqui, vamos focar no Ubuntu.

Pré-requisitos:

Atualize o sistema e remova versões antigas do Docker, se houver:
lua
Copy code
sudo apt update && sudo apt upgrade
sudo apt remove docker docker-engine docker.io containerd runc
Instale os pacotes necessários para o Docker:
arduino
Copy code
sudo apt-get install apt-transport-https ca-certificates curl gnupg lsb-release
Adicionar o Repositório do Docker:

Configure o repositório do Docker:
bash
Copy code
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
Instalar o Docker Engine:

Atualize a lista de pacotes e instale o Docker:
sql
Copy code
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
Permissões:

Adicione seu usuário ao grupo do Docker para executar comandos do Docker sem necessitar de sudo:
bash
Copy code
sudo usermod -aG docker $USER
Reinicie o WSL para aplicar as mudanças:
arduino
Copy code
wsl --shutdown
Inicie o serviço Docker:
sql
Copy code
sudo service docker start
Configurar o Docker para Iniciar com o WSL:

No Windows 11, você pode configurar o WSL para iniciar o Docker automaticamente:
bash
Copy code
sudo vim /etc/wsl.conf
No arquivo, adicione:
bash
Copy code
[boot]
command = service docker start
Salve e feche o arquivo, e reinicie o WSL.
Verificar a Instalação:

Teste a instalação com:
Copy code
docker ps
Docker Desktop como Alternativa
Se preferir uma interface gráfica, você pode optar por usar o Docker Desktop.

Instalação:

Baixe o Docker Desktop do site oficial e instale.
Configuração:

Abra o Docker Desktop.
Acesse Settings > Resources > WSL Integration.
Habilite a integração com sua distro Linux padrão.
Dicas de Uso do WSL2
Evite armazenar projetos no caminho /mnt/c para melhor performance.
Acesse o sistema de arquivos do Linux no Windows usando \\wsl$ no File Explorer.
Use code . no WSL para abrir arquivos no VS Code.
Libere memória no WSL com o comando: echo 1 | sudo tee /proc/sys/vm/drop_caches.
Resolução de Problemas
Se encontrar o erro "Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?", tente usar iptables-legacy:

sql
Copy code
sudo update-alternatives --config iptables
Escolha iptables-legacy e reinicie o serviço Docker.

Recursos Adicionais
Para mais dicas de produtividade no Windows e guias de configuração de ambiente, confira:

Ambiente de Desenvolvimento Produtivo
Configuração do VSCode
Espero que este guia unificado seja útil para configurar e aproveitar o WSL2 e o Docker no seu sistema Windows!
