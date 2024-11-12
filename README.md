# Guia Prático Docker - Primeiros Passos

## Habilitar virtualização BIOS
- Reinicie o computador e entre na configuração do BIOS/UEFI (geralmente pressionando Del, F2, ou F10 durante a inicialização, dependendo do fabricante).
- Procure por uma opção relacionada à Virtualização ou Intel VT-x/AMD-V e habilite-a.

### Passo a passo BIOS sem desligar
1. Configurações Window Update
2. Recuperação
3. Simular Restauração PC - Começar agora
4. Solução de Problemas
5. 

## Hyper-V para WSL (Opção Windows Home Edition)
 - Habilitar a "Plataforma da Máquina Virtual"
 - Abra o Prompt de Comando ou PowerShell como administrador.

```sh 
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

## Instalar WSL e uma distribuição Linux
No Prompt de Comando ou PowerShell (como administrador), execute:
```sh 
wsl --install
```

Se o WSL já estiver instalado, certifique-se de que a versão padrão é a WSL2:
```sh 
wsl --set-default-version 2
```

Confirmar se o WSL2 está habilitado e funcionando corretamente.
```sh 
wsl --status
```

Lista das distribuições Linux disponíveis para download
```sh
wsl --list --online
```

Instalar Distribuição [Ubuntu 18.04 LTS]
```sh
wsl --install -d <Distribution Name>
```

[Opcional] Executar ambiente virtual WSL no terminal
```sh
wsl.exe
```

## Trabalahndo com Linux [Ubuntu 22.04]
### Instalar Docker e Docker Compose

- Verificar versão instalada
```sh
lsb_release -a
```

- Atualizar sistema e instalar pacotes necessários
```sh
sudo apt update
sudo apt upgrade -y
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
```

- Adicione a chave GPG do Docker e o repositório oficial

Crie o diretório de keyrings, se não existir:
```sh
sudo mkdir -p /etc/apt/keyrings
```

Rebaixe a chave pública do Docker e armazene-a no novo keyring:
```sh
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo tee /etc/apt/keyrings/docker.gpg > /dev/null
```

Atualize a lista de pacotes:
```sh
sudo apt update
```

- Verificar a chave GPG adicionada
```sh
sudo apt-key list
```

- Instale o Docker
```sh
sudo apt update
sudo apt install -y docker-ce
```

- Verifique a instalação Docker
```sh
docker --version
```

- Baixe a versão mais recente do Docker Compose
```sh
sudo apt update
sudo apt install jq
sudo curl -L "https://github.com/docker/compose/releases/download/$(curl -s https://api.github.com/repos/docker/compose/releases/latest | jq -r .tag_name)/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

- Dê permissão de execução (Docker-Compose)
```sh
sudo chmod +x /usr/local/bin/docker-compose
```

- Verifique a instalação (Docker-Compose)
```sh
docker-compose --version
```

### Instalando Python e suas dependências
- Verifique a versão do python isntalada
```sh
python3 --version
```

- Instalar pacote pip Python
```sh
sudo apt install python3-pip
```

- Instalar ambiente virtual
```sh
sudo apt-get install python3-venv
```

- Build Tools que podem ser utilizadas
```sh
sudo apt update
sudo apt-get install build-essential python3-dev
```

- Atualize os links simbólicos do Python
```sh
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.9 1
```

### Instalando Bibliotecas de Desenvolvimento PostgreSQL 
- Esses pacotes fornecem utilitários de linha de comando para administração e scripts:
```sh
sudo apt install postgresql postgresql-contrib
sudo apt-get install postgresql-client
```

- Drivers e bindings para Python
```sh
sudo apt-get install python3-psycopg2
pip install psycopg2
```

- Arquivos de cabeçalho (headers) e bibliotecas de desenvolvimento necessários para compilar programas que interagem com o PostgreSQL
```sh
sudo apt-get install libpq-dev
```

- Verifique a instalação PostgresSQL
```sh
psql --version
```

### Instalando Git 
- Certificar se o Git está instalado
```sh
sudo apt update
sudo apt install git
```

- Verifique a instalação Git
```sh
git --version
```

### Criação de Diretórios
- Para criar um diretório
```sh
sudo mkdir -p /home/projects/caminho/arquivo
ls /home/projects/caminho/arquivo
```

- Para excluir diretórios vazios
```sh
rmdir /caminho/para/o/diretorio
```

- Excluir um diretório não vazio
```sh
rm -r /caminho/para/o/diretorio
```

### Inicializando o VS Code
- Baixar e instalar VS Code
```sh
sudo snap install --classic code
```

- Para abrir o VS Code através do terminal Ubunto
```sh
code
```

#### VS Code com WSL Distro Ubunto
- Abrir, editar e rodar projetos diretamente no ambiente Linux do WSL (Ubunto) com o VS Code
- Barra de comandos VS Code [Ctrl + P > WSL: Connect to WSL using Distro...]
- Selecionar a Distro Ubuntu 22.04 que está baixada e configurada
- Ao conectar com WSL uma janela Remota será aberta, em que uma nova pasta será vinculada e as extensões devem ser instaladas novamente, caso já tiverem sido instaladas localmente.
* Com excessão da Extensão WSL (deve ser instalada apenas LOCALMENTE)

#### Extensões Principais
1. Docker
2. Python
3. Python Lint
4. Python Debuggers
5. PostgreSQL
6. WSL

#### Abrir diretório do projeto correspondente
- Após configurar conexão WSL e Ubunto no VS Code, abrir diretório do porjeto ou algum repositório do GitHub previamente clonado através do terminal

#### Clonando Repositório
- Acesse o diretório onde deseja clonar o repositório
```sh
cd /caminho/do/diretorio
```

- Clone o repositório
```sh
git clone https://github.com/vitorvogomes/fastapi-stand-livros.git
ls
```

- Verifique as permissões do diretório
```sh
ls -ld /caminho/do/diretorio
sudo chown -R $USER:$USER /caminho/do/diretorio
```

- Configure as variáveis globais de nome e email no Git
```sh
git config --global user.email "vitorgomes190@gmail.com"
git config --global user.name "Vitor Gomes"
```

- Acesse o diretório do repositório clonado
```sh
cd repositorio
```

- Caso queira configurar variáveis locais de nome e email para este repositório
```sh
git config user.email "outroemail@exemplo.com"
git config user.name "Outro Nome"
```

- Verifique as configurações do Git
```sh
git config --list
```

#### Python no VS Code
- A extensão Python detectará automaticamente o interpretador Python do WSL.
- Aba de comando VS Code [Ctrl+Shift+P → Python: Select Interpreter]

- Criar ambiente virtual
```sh
python3 -m venv .venv
```

- Inicializar o ambiente virtual
```sh
source .venv/bin/activate
```
- Atualizar ferramentas pip
```sh
python3 -m pip install --upgrade pip
```

- Download das dependencias do projeto
```sh
pip install -r requirements.txt
```

- Atualizar ferramentas pip 
```sh
pip install --upgrade pip setuptools wheel
```

#### Conectar PostgreSQL e variáveis de ambiente
- Criar um arquivo .env com os parâmtros de conexão do banco de dados
```sh
POSTGRES_USER=seu_usuario
POSTGRES_PASSWORD=sua_senha
POSTGRES_DB=seu_banco
DATABASE_URL=postgresql://seu_usuario:sua_senha@db:5432/seu_banco
```

- Aba de comando VS Code [Ctrl + P > PostgreSQL: Add Connection]
- Inserir "host" -> "Localhost"
- Inserir "seu_usuario" -> "seu_usuario"
- Inserir "sua_senha" -> "sua_senha"
- Inserir "port" -> "5432"
- Inserir "seu_banco" -> "seu_banco"


#### Configuração do Docker no VS Code
- Criar um novo terminal dentro do endereço do projeto correspondente, no VS Code
- Verificar se o Docker está funcionando
```sh
sudo service docker status
sudo service docker start
```

- Adicionar seu usuário ao grupo docker. Permitir que seu usuário acesse o Docker sem usar "sudo", você precisa adicionar o usuário ao grupo docker
```sh
sudo usermod -aG docker $USER
groups $USER
```

- Testar o comando
```sh
docker ps
```

#### Docker Compose para incializar os Containers
- Logs: Para verificar logs e garantir que tudo está correto
```sh
docker-compose logs
docker-compose logs <container>
```

- Build Down: Rebuild e Restart nos containers
```sh
docker-compose down
```

- Build e Up: Para criar os containers
```sh
docker-compose up --build
```

- Up: Para inicializar os containers
```sh
docker-compose up
```

#### Versões utilizadas no projeto

Ubuntu 24.04.1 LTS
Python 3.12.3
Docker 27.3.1
Docker Compose version v2.30.3
PostgreSQL 16.4 (Ubuntu 16.4-0ubuntu0.24.04.2)