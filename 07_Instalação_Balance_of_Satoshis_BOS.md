# Instalação

Balance of Satoshis (BOS)
Este tutorial irá guiá-lo na instalação do Balance of Satoshis (bos), uma
ferramenta que auxilia na monitorização de um node Lightning e oferece funcionalidades de administração.
Certifique-se de ter um sistema baseado em Debian/Ubuntu e que o Node.js
esteja instalado. Você também precisará de acesso root ou permissões de

````bash sudo.
``` Veja aqui para instalar os pré-requisitos.
Execute os comandos abaixo para atualizar o sistema e instalar o Node.js:
```bash curl -sL https://deb.nodesource.com/setup_21.x| sudo -E bash -
````

````bash sudo apt-get install nodejs -y
``` Crie um diretório para o npm global e configure o prefixo:
Adicione o caminho do npm global ao PATH no arquivo ~/.profile :
Carregue o perfil atualizado:
Instale o bos globalmente:
Verifique a instalação:
Adicione a seguinte linha ao arquivo /etc/hosts :
```bash
mkdir -p ~/.npm-global
npm config set prefix '~/.npm-global'
if ! grep -q 'PATH="$HOME/.npm-global/bin:$PATH"' ~/.profile; then echo 'PATH="$HOME/.npm-global/bin:$PATH"' >> ~/.profile; fi
source ~/.profile
npm i -g balanceofsatoshis
bos --version
````

````bash sudo bash -c 'echo "127.0.0.1 localhost" >> /etc/hosts'
``` Ajuste as permissões do diretório LND (verifique o caminho correto do seu diretório LND
Substitua /data/lnd pelo caminho do seu diretório LND e execute:
Substitua nome_do_seu_node pelo nome que deseja dar ao seu node e crie o diretório:
Gere os arquivos base64 (verifique o caminho correto para o seu certificado e macaroon):
```bash sudo chown -R $USER:$USER /data/lnd
````

````bash sudo chmod -R 755 /data/lnd
``` export BOS_DEFAULT_LND_PATH=/data/lnd
```bash mkdir -p ~/.bos/nome_do_seu_node
``` base64 -w0 /data/lnd/tls.cert > /data/lnd/tls.cert.base base64 -w0 /data/lnd/data/chain/bitcoin/mainnet/admin.macaroon > /
data/lnd/data/chain/bitcoin/mainnet/admin.macaroon.base Substitua seu_node pelo nome do seu node e crie o arquivo credentials.json com os valores codificados em base64 Para testar a instalação, execute o seguinte comando:
Crie o arquivo de serviço bos-telegram.service , substituindo ID_TELEGRAM
pelo seu código no Telegram: Você pode obter o seu ID no Telegram pelo bot @userinfobot e comando /start )
```bash
cert_base64=$(cat /data/lnd/tls.cert.base64)
macaroon_base64=$(cat /data/lnd/data/chain/bitcoin/mainnet/admin.macaroon.base64)
cat <<EOF > ~/.bos/seu_node/credentials.json
{
  "cert": "$cert_base64",
  "macaroon": "$macaroon_base64",
  "socket": "localhost:10009"
}
EOF
``` bos utxos
## ID_TELEGRAM Atualize o daemon do systemd para reconhecer o novo serviço:
Inicie o serviço:
```bash sudo bash -c "cat <<EOF > /etc/systemd/system/bos-telegram.service
````

# Systemd

unit for Bos-Telegram Bot

# /etc/systemd/system/bos-telegram.service [Unit] Description=bos-telegram Wants=lnd.service After=lnd.service [Service] ExecStart=/home/admin/.npm-global/bin/bos telegram --use-small-units --connect ID_TELEGRAM User=admin Restart=always TimeoutSec= RestartSec= StandardOutput=null StandardError=journal Environment=BOS_DEFAULT_LND_PATH=/data/lnd [Install] WantedBy=multi-user.target

## EOF"

```bash sudo systemctl daemon-reload

```

````bash sudo systemctl start bos-telegram.service
``` Habilite o serviço para iniciar automaticamente ao ligar o sistema:
Verifique se o serviço está ativo:
Se o serviço estiver como <active> , tudo correu bem. Pressione Ctrl + C para voltar ao terminal.
A instalação do Balance of Satoshis (bos) foi concluída com sucesso! Agora você pode executar o comando:
para configurar o monitoramento pelo Telegram.
Atenção: Caso ainda não tenha criado o seu Bot no Telegram, você deve criá-lo acessando o bot @botfather e comando /start
Substitua BOT_API_KEY pela API KEY do seu bot do Telegram.
Fim.
Anterior
```bash sudo systemctl enable bos-telegram.service
````

````bash sudo systemctl status bos-telegram.service
``` bos telegram
## Acesso Remoto via Tor (opcional)
Próximo
## Instalação LNDHub (opcional)
Atualizado há 9 meses
````
