# Instalação
 LNDHub (opcional)
Contribuição Cassiano Primo Membro BR
LN Este tutorial guia você pela instalação e configuração do LNDHub, uma
interface para gerenciar carteiras Lightning Network. O processo inclui a
## instalação do Redis, configuração do LNDHub e inicialização do serviço.
O Redis é necessário para o funcionamento do LNDHub. Siga os passos abaixo para instalá-lo:
Inicie o Redis e habilite-o para iniciar automaticamente na inicialização do sistema:
Verifique o status do Redis para confirmar que ele está em execução:
```bash sudo apt update
```
```bash sudo apt install redis
```
```bash sudo systemctl start redis
```
```bash sudo systemctl enable redis
```
```bash sudo systemctl status redis
``` Clone o repositório do LNDHub:
Instale as dependências do projeto:
Crie o arquivo de configuração config.js :
Adicione o seguinte conteúdo:
```bash git clone https://github.com/BlueWallet/LndHub.git```
```bash cd LndHub
``` npm install
```bash nano config.js
``` config.js
Se você estiver usando um Bitcoin Core local, substitua o bloco bitcoind no config.js pelo seguinte:
let config = {
host: '0.0.0.0', // Ou o IP ou o domínio do seu servidor port: 4000, // Definindo a porta para enableUpdateDescribeGraph: false, postRateLimit: 100, rateLimit: 200, forwardReserveFee: 0.01, // Taxa padrão de 0.
intraHubFee: 0.003, // Taxa padrão de 0.
// Configuração para Bitcoin Core remoto
```bash bitcoind: {
``` rpc: 'http:// usuario_exemplo:senha_exemplo@bitcoin.com:8085', zmqpubrawblock: 'tcp://bitcoin.com:28332', zmqpubrawtx: 'tcp://bitcoin.com:28333', // Configuração para Redis redis: { port: 6379, host: '127.0.0.1', family: 4, db: 0, // Configuração para LND
```bash lnd: {
``` url: '127.0.0.1:10009', password: 'senha_do_lnd', // Substitua pela senha do LND cert: '/data/lnd/tls.cert' // Caminho para o arquivo tls.cert module.exports = config; Crie ou edite o arquivo lightning.js :
Adicione o seguinte conteúdo:
```bash bitcoind: {
``` rpc: 'file:///home/admin/.bitcoin/.cookie', zmqpubrawblock: 'tcp://127.0.0.1:28332', zmqpubrawtx: 'tcp://127.0.0.1:28333',
```bash nano /home/admin/LndHub/lightning.js
``` const config = require('./config'); const fs = require('fs'); const grpc = require('@grpc/grpc-js'); const protoLoader = require('@grpc/proto-loader'); const loaderOptions = { keepCase: true, longs: String, enums:
String, defaults: true, oneofs: true }; const packageDefinition = protoLoader.loadSync('rpc.proto', loaderOptions); const lnrpc = grpc.loadPackageDefinition(packageDefinition).lnrpc; let lndCert = fs.readFileSync('/data/lnd/tls.cert'); let sslCreds = grpc.credentials.createSsl(lndCert); let macaroon = fs.readFileSync('/data/lnd/ admin.macaroon').toString('hex'); let macaroonCreds = grpc.credentials.createFromMetadataGenerator((args, callback) => { let metadata = new grpc.Metadata(); metadata.add('macaroon', macaroon); callback(null, metadata); }); let creds = grpc.credentials.combineChannelCredentials(sslCreds, macaroonCreds); module.exports = new lnrpc.Lightning(config.lnd.url, creds, { 'grpc.max_receive_message_length': 1024 * 1024 * 1024 }); lightning.js Navegue até o diretório do LNDHub:
Inicie o LNDHub:
Crie um arquivo de teste:
Adicione o seguinte código:
Execute o teste:
Crie um arquivo de serviço para o LNDHub:
```bash cd LndHub
``` npm start
```bash nano test.js
``` const fs = require('fs'); try { const cert = fs.readFileSync('/data/lnd/tls.cert'); console.log('Certificado lido com sucesso!'); } catch (error) { console.error('Erro ao ler o certificado:', error.message); node test.js tls.cert systemd Adicione o seguinte conteúdo:
Salve e saia do editor CTRLX, Y, ENTER.
Recarregue as configurações do systemd :
Inicie o serviço LNDHub:
Habilite o serviço para iniciar automaticamente na inicialização do sistema:
Verifique o status do serviço:
```bash sudo nano /etc/systemd/system/lndhub.service
``` [Unit] Description=LndHub After=network.target [Service] WorkingDirectory=/home/admin/LndHub ExecStart=/usr/bin/npm start Restart=always User=admin Group=admin Environment=NODE_ENV=production [Install] WantedBy=multi-user.target
```bash sudo systemctl daemon-reload
```
```bash sudo systemctl start lndhub.service
```
```bash sudo systemctl enable lndhub.service
```
```bash sudo systemctl status lndhub.service
``` Agora seu LNDHub está instalado e configurado!
Anterior
## Instalação Balance of Satoshis BOS Atualizado há 8 meses
```bash sudo ufw allow 4000/tcp
```
```bash sudo ufw reload
```
```bash sudo ufw status
```
