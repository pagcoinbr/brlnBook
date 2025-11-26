# Instalação
 do LND
Vamos configurar o LND, o Lightning Network Daemon da Lightning Labs.
- Postgresql Minibolt Tutorial)
A instalação do LND é simples, mas a aplicação é bastante poderosa e capaz
de fazer coisas que não são explicadas aqui. Confira o repositório deles no
GitHub para obter uma quantidade enorme de informações sobre o projeto
de código aberto e sobre a Lightning Network em geral.
Antes de executar o LND, precisamos configurar as definições no arquivo de
## configuração do Bitcoin Core para habilitar a conexão RPC do LND.
Faça login como usuário bitcoin, edite o arquivo bitcoin.conf Adicione as seguintes linhas. Salve e saia.
Reinicie o Bitcoin Core para aplicar as alterações.
Verifique se o Bitcoin Core ativou zmqpubrawblock e zmqpubrawtx nas portas 28332 e 28333.
Saída esperada:
Vamos baixar, verificar e instalar o LND. Navegue até o diretório temporário.
```bash sudo su - bitcoin
```
```bash nano /data/bitcoin/bitcoin.conf
```
# Enable
 ZMQ raw notification (for LND)
zmqpubrawblock=tcp://127.0.0.1:
zmqpubrawtx=tcp://127.0.0.1:
exit
```bash sudo systemctl restart bitcoind
```
```bash sudo ss -tulpn | grep LISTEN | grep bitcoind | grep
``` > tcp LISTEN 0 100 127.0.0.1:28332 0.0.0.0:* users:(("bitcoind",pid=773834,fd=20)) > tcp LISTEN 0 100 127.0.0.1:28333 0.0.0.0:*
users:(("bitcoind",pid=773834,fd=22)) Defina uma variável de ambiente temporária para a instalação.
Baixe o aplicativo, checksums e assinatura.
Verifique o checksum assinado em relação ao checksum real do seu download Exemplo de saída esperada:
```bash cd /tmp
```
## VERSION=0.20.
```bash wget https://github.com/lightningnetwork/lnd/releases/download/``` v$VERSION-beta/lnd-linux-amd64-v$VERSION-beta.tar.gz
```bash wget https://github.com/lightningnetwork/lnd/releases/download/``` v$VERSION-beta/manifest-v$VERSION-beta.txt.ots
```bash wget https://github.com/lightningnetwork/lnd/releases/download/``` v$VERSION-beta/manifest-v$VERSION-beta.txt
```bash wget https://github.com/lightningnetwork/lnd/releases/download/``` v$VERSION-beta/manifest-roasbeef-v$VERSION-beta.sig.ots
```bash wget https://github.com/lightningnetwork/lnd/releases/download/``` v$VERSION-beta/manifest-roasbeef-v$VERSION-beta.sig sha256sum --check manifest-v$VERSION-beta.txt --ignore-missing > lnd-linux-amd64-v0.19.3-beta.tar.gz: OK
Agora que verificamos a integridade do binário baixado, precisamos verificar
a autenticidade do arquivo de manifesto que acabamos de usar, começando com a sua assinatura.
Obtenha a chave pública de um desenvolvedor do LND, que assinou o
arquivo de manifesto; e adicione-a ao seu anel de chaves GPG.
Saída esperada:
Verifique a assinatura do arquivo de texto contendo os checksums para a aplicação.
Exemplo de saída esperada:
```bash curl https://raw.githubusercontent.com/lightningnetwork/lnd/``` master/scripts/keys/roasbeef.asc | gpg --import
> % Total % Received % Xferd Average Speed Time Time Time Current > Dload Upload Total Spent Left Speed
> 100 6900 100 6900 0 0 19676 0 --:--:-- --:--:--
--:--:-- > gpg: key 372CBD7633C61696: "Olaoluwa Osuntokun <laolu32@gmail.com>" imported > gpg: Total number processed:
> gpg: unchanged:
gpg --verify manifest-roasbeef-v$VERSION-beta.sig manifest-v$VERSION-beta.txt

Também podemos verificar se o arquivo de manifesto estava em existência na época do lançamento usando seu timestamp.
Vamos verificar se o timestamp do arquivo corresponde à data de lançamento.
Exemplo de saída esperada:
> gpg: Signature made Mon 13 Nov 2023 11:45:38 PM UTC > gpg: using RSA key
## 60A1FA7DA5BFF08BDCBBE7903BBD59E99B > gpg: Good signature from "Olaoluwa Osuntokun <laolu32@gmail.com>" [unknown]
> gpg: WARNING: This key is not certified with a trusted
signature! > gpg: There is no indication that the signature belongs to the owner.
> Primary key fingerprint: E4D8 5299 674B 2D31 FAA1 892E 372C
## BD76 33C6
> Subkey fingerprint: 60A1 FA7D A5BF F08B DCBB E790 3BBD
## 59E9 9B28 ots --no-cache verify manifest-roasbeef-v$VERSION-beta.sig.ots -f manifest-roasbeef-v$VERSION-beta.sig > Got 1 attestation(s) from https:// alice.btc.calendar.opentimestamps.org > Got 1 attestation(s) from https://btc.calendar.catallaxy.com> Got 1 attestation(s) from https:// finney.calendar.eternitywall.com > Got 1 attestation(s) from https://
bob.btc.calendar.opentimestamps.org > Success! Bitcoin block 765521 attests existence as of 2022-12-UTC ots --no-cache verify manifest-v$VERSION-beta.txt.ots -f manifest-v$VERSION-beta.txt Exemplo de saída esperada:
Verifique se a data do timestamp está próxima da data de lançamento do binário do LND.
Tendo verificado a integridade e autenticidade do binário de lançamento, podemos prosseguir com a extração.
Exemplo de saída esperada:
Instale-o.
Verifique se a instalação foi bem-sucedida executando o comando de versão.
> Got 1 attestation(s) from https:// alice.btc.calendar.opentimestamps.org > Got 1 attestation(s) from https://btc.calendar.catallaxy.com> Got 1 attestation(s) from https:// finney.calendar.eternitywall.com > Got 1 attestation(s) from https://
bob.btc.calendar.opentimestamps.org > Success! Bitcoin block 829257 attests existence as of 2024-02-UTC tar -xvf lnd-linux-amd64-v$VERSION-beta.tar.gz > lnd-linux-amd64-v0.19.3-beta/lnd > lnd-linux-amd64-v0.19.3-beta/lncli > lnd-linux-amd64-v0.19.3-beta/
```bash sudo install -m 0755 -o root -g root -t /usr/local/bin lnd-linux-
``` amd64-v$VERSION-beta/lnd lnd-linux-amd64-v$VERSION-beta/lncli Exemplo de saída esperada:
Se você chegou até aqui, esta é a etapa final.
Crie o usuário e grupo lnd .
Adicione o usuário lnd aos grupos "bitcoin" e "debian-tor", permitindo que
o usuário btcrpcexplorer leia o arquivo .cookie do bitcoind e utilize a porta de controle configurando o Tor diretamente.
Adicione o usuário admin ao grupo "lnd".
Crie a pasta de dados do LND.
```bash lnd --version
``` > lnd version 0.19.3-beta commit=v0.19.3-beta
```bash sudo rm -r lnd-linux-amd64-v$VERSION-beta lnd-linux-amd64-
``` v$VERSION-beta.tar.gz manifest-roasbeef-v$VERSION-beta.sig manifest-roasbeef-v$VERSION-beta.sig.ots manifest-v$VERSION-beta.txt manifest-v$VERSION-beta.txt.ots
```bash sudo adduser --disabled-password --gecos "" lnd
```
```bash sudo usermod -a -G bitcoin,debian-tor lnd
```
```bash sudo adduser admin lnd
``` Atribua a propriedade ao usuário lnd .
Abra uma sessão de usuário lnd .
Crie links simbólicos apontando para os diretórios de dados do LND e Bitcoin.
Verifique se os links simbólicos foram criados corretamente.
Saída esperada:
```bash sudo mkdir /data/lnd
```
```bash sudo chown -R lnd:lnd /data/lnd
```
```bash sudo su - lnd
``` ln -s /data/lnd /home/lnd/.lnd ln -s /data/bitcoin /home/lnd/.bitcoin ls -la
total drwxr-x--- 2 lnd lnd 4096 Jul 15 20:57 .
drwxr-xr-x 7 root root 4096 Jul 15 20:54 ..
-rw-r--r-- 1 lnd lnd 220 Jul 15 20:54 .bash_logout
-rw-r--r-- 1 lnd lnd 3771 Jul 15 20:54 .bashrc
lrwxrwxrwx 1 lnd lnd 13 Jul 15 20:57 .bitcoin -> /data/bitcoin
lrwxrwxrwx 1 lnd lnd 9 Jul 15 20:56 .lnd -> /data/lnd
-rw-r--r-- 1 lnd lnd 807 Jul 15 20:54 .profile
O LND inclui uma carteira Bitcoin que gerencia suas moedas onchain e
Lightning. Ela é protegida por senha e deve ser desbloqueada quando o LND
inicia. Isso cria o dilema de ter que desbloquear o LND manualmente após
cada reinicialização do seu PC, ou armazenar a senha em algum lugar no nó.
Para esta configuração inicial, escolhemos a rota mais fácil: armazenamos a
senha em um arquivo que permite ao LND desbloquear a carteira automaticamente.
Ainda como usuário lnd , crie um arquivo de texto e insira sua senha de
carteira do LND C. A senha deve ter pelo menos 8 caracteres. Salve e saia.
Restringa as permissões de acesso e faça com que o arquivo seja legível apenas pelo usuário lnd .
Crie o arquivo de configuração do LND.
Cole o seguinte conteúdo (defina seu alias <NOME_DO_NODE> , sua cor
preferida <#ff9900> , o tamanho mínimo do canal minchansize e as taxas).
Salve e saia.
```bash nano /data/lnd/password.txt
```
```bash chmod 600 /data/lnd/password.txt
```
```bash nano /data/lnd/lnd.conf
```
# LND
 Independente: configuração do lnd
# /data/lnd/lnd.conf [Application Options]
# Até
 32 caracteres UTF-8, aceita emojis, por exemplo alias=<NOME_DO_NODE>
# Você
 pode escolher a cor que deseja em https://www.color-hex.com/color=#ff debuglevel=info
# Desbloquear
 automaticamente a carteira com a senha neste arquivo wallet-unlock-password-file=/data/lnd/password.txt wallet-unlock-allow-create=true
# Regenerar
 automaticamente o certificado quando estiver próximo do vencimento tlsautorefresh=true tlsextraip=127.0.0.
## Configurações de canais
# (Opcional) Tamanho mínimo do canal. Descomente e defina conforme desejar
# (padrão: 20000 sats)
#minchansize=
## Configurações de ambiente de alta taxa (Opcional)
#max-commit-fee-rate-anchors=
#max-channel-fee-allocation=0.
## Comunicação accept-keysend=true accept-amp=true
## Rebalanceamento allow-circular-route=true
## Performance sync-freelist=false gc-canceled-invoices-on-startup=true gc-canceled-invoices-on-the-fly=true ignore-historical-gossip-filters=true
# Se

você tem um node com mais de 75 canais, dobre o valor abaixo de 100 para num-restricted-slots=
## Clearnet - Descomentar e configurar as linhas abaixo - Opte por usar o servico Clearnet do clube usar o servico Clearnet do clube
#listen=0.0.0.0:
#IP externo publico - Caso tenha IP public descomente a linha abaixo
#externalip=ip_externo:porta
#DDNS - Caso use um servico de DDNS ou tenha um dominio descomentar a linha abaixo
#externalhosts=nome_dominio:porta [Bitcoin]
```bash bitcoin.mainnet=true
```
```bash bitcoin.node=bitcoind
```
# Configurações

de taxa - taxa base padrão do LND = 1000 (mSat), taxa de comissão = 1 (ppm)
# Você
 pode escolher o que quiser, por exemplo, ZeroFeeRouting (0,0) ou ZeroBaseFee (0,X)
```bash bitcoin.basefee=
```
```bash bitcoin.feerate=
```
# (Opcional) Especifique o delta CLTV que subtrairemos do valor de timelock de um HTLC encaminhado
# (padrão: 80)
```bash bitcoin.timelockdelta=
``` [wtclient]
## Configurações do cliente Watchtower wtclient.active=true
# (Opcional) Especifique a taxa de comissão com a qual as transações de justiça serão assinadas
# (padrão: 10 sat/byte)
wtclient.sweep-fee-rate=
#[watchtower]
## Configurações do servidor Watchtower - Opcional, descomente se quer que essa instalação seja um Tower
#watchtower.active=true [routing] routing.strictgraphpruning=true
## Descomente as linhas abaixo se você pretende utilizar o postgresql como banco de dados [db]
## Banco de dados db.backend=postgres [postgres] db.postgres.dsn=postgresql://admin:admin@127.0.0.1:5432/lndb? sslmode=disable db.postgres.timeout=
## Comente as linhas se pretende usar o postgresql como banco de dados
#[bolt]
## Database
# Set
 the next value to false to disable auto-compact DB
# and
 fast boot and comment the next line
#db.bolt.auto-compact=true
# Uncomment

to do DB compact at every LND reboot (default: 168h)
#db.bolt.auto-compact-min-age=0h
## Ambiente de alta taxa (Opcional)
# (padrão: CONSERVATIVE) Descomente as próximas 2 linhas [Bitcoind]
```bash bitcoind.estimatemode=ECONOMICAL
```
#bitcoind local - mesma maquina
```bash bitcoind.rpcuser=<seu_user_rpc>
```
```bash bitcoind.rpcpass=<sua_senha_rpc>
```
```bash bitcoind.zmqpubrawblock=tcp://127.0.0.1:
```
```bash bitcoind.zmqpubrawtx=tcp://127.0.0.1:
```
## ATENCAO: Para bitcoin Externo como o da BRLN Comente as quatro linhas acima e descomente as 5 abaixo.
#bitcoind.rpchost=bitcoin.br-ln.com:
#bitcoind.rpcuser=<seu_user_rpc>
#bitcoind.rpcpass=<sua_senha_rpc>
#bitcoind.zmqpubrawblock=tcp://bitcoin.br-ln.com:
#bitcoind.zmqpubrawtx=tcp://bitcoin.br-ln.com:
[routerrpc] routerrpc.estimator=apriori routerrpc.minrtprob=0.
routerrpc.apriori.hopprob=0.
routerrpc.apriori.weight=0.
routerrpc.apriori.penaltyhalflife=2h routerrpc.attemptcost= routerrpc.attemptcostppm= routerrpc.maxmchistory=
# Se

você tem um node com mais de 75 canais sugestao é dobrar os valores abaixo [gossip] gossip.msg-rate-bytes= gossip.msg-burst-bytes= [caches] caches.channel-cache-size= caches.reject-cache-size= caches.rpc-graph-cache-duration=10m [rpcmiddleware] rpcmiddleware.enable=true [tor] tor.active=true tor.v3=true
## Se for usar clearnet troque para true e false as linhas abaixo respectivamente tor.skip-proxy-for-clearnet-targets=false
tor.streamisolation=true Esta é uma configuração padrão. Verifique o sample-lnd.conf oficial do
LND com todas as opções possíveis se você quiser adicionar algo especial.
Para configurar o seu node para acesso via Clearnet, vá para esse tutorial complementar:
Saia da sessão do usuário lnd para retornar à sessão do usuário admin.
Agora, vamos configurar o LND para iniciar automaticamente na inicialização do sistema.
Como usuário admin , crie a unidade systemd do LND.
Insira o conteúdo completo a seguir. Salve e saia.
exit
```bash sudo nano /etc/systemd/system/lnd.service
```
# LND: unidade systemd para lnd
# /etc/systemd/system/lnd.service [Unit] Description=Lightning Network Daemon Requires=bitcoind.service After=bitcoind.service [Service] ExecStart=/usr/local/bin/lnd ExecStop=/usr/local/bin/lncli stop
# Gerenciamento
 de processo
#################### Restart=on-failure RestartSec= Type=notify TimeoutStartSec= TimeoutStopSec=
# Criação
 e permissões de diretório
#################################### RuntimeDirectory=lightningd RuntimeDirectoryMode= User=lnd Group=lnd
# Medidas
 de proteção
#################### PrivateTmp=true ProtectSystem=full NoNewPrivileges=true PrivateDevices=true MemoryDenyWriteExecute=true [Install] WantedBy=multi-user.target
```bash sudo systemctl enable lnd
``` Agora, as informações do daemon não são mais exibidas na linha de
comando, mas são registradas no journal do sistema. Você pode verificá-las
## usando o comando a seguir. Você pode sair do monitoramento a qualquer momento com Ctrl-C.
Para acompanhar os movimentos do software, inicie seu programa SSH (por
exemplo, PuTTY) uma segunda vez, conecte-se ao nó MiniBolt e faça login como admin .
Inicie o serviço.
Assim que o LND for iniciado, o processo aguardará que criemos a carteira Bitcoin onchain integrada.
Altere para o usuário lnd .
Crie a carteira do LND.
Saída esperada:
journalctl -fu lnd
```bash sudo systemctl start lnd
```
```bash sudo su - lnd
``` lncli create Input wallet password:
Confirm password:
Digite sua senha C] como senha da carteira 2 vezes (deve ser a mesma que
você armazenou no arquivo password.txt na etapa de Senha da carteira).
Saída esperada:
Pressione n e confirme.
Se você escolher esta opção, o próximo passo será escolher a frase secreta
(opcional - pressione enter para prosseguir sem uma frase secreta de seed cipher).
Saída esperada:
Digite a frase secreta e pressione enter [o prompt solicitará que você digite
sua senha C] mais uma vez Confirm password:)] ou, se optar por não usar a frase secreta, pressione enter simplesmente.
Exemplo de saída esperada:
Do you have an existing cipher seed mnemonic or extended master root key you want to use?
Enter 'y' to use an existing cipher seed mnemonic, 'x' to use an extended master root key or 'n' to create a new seed (Enter y/x/n):
Your cipher seed can optionally be encrypted.
Input your passphrase if you wish to encrypt it (or press enter to proceed without a cipher seed passphrase):
Essas 24 palavras são tudo o que você precisa (e o arquivo channel.backup
em caso de recuperação de desastre) para restaurar a carteira Bitcoin onchain e possíveis UTXOs bloqueados.
Anote essas 24 palavras manualmente em um pedaço de papel e guarde-o em um local seguro.
Você pode usar um simples pedaço de papel, escrevê-las em um cartão de
backup temático da Shiftcrypto, ou até mesmo gravar as palavras da seed em metal.
Esse pedaço de papel é tudo o que um invasor precisa para esvaziar sua carteira on-chain!
Não armazene em um computador.
Não tire uma foto com seu celular.
Esta informação nunca deve ser armazenada em formato digital.
Esta informação deve ser mantida em segredo o tempo todo.
Retorne ao primeiro terminal com journalctl -fu lnd . Exemplo de saída esperada Generating fresh cipher seed...
## !!!VOCÊ DEVE ANOTAR ESTA SEED PARA PODER RESTAURAR A CARTEIRA!!!
## ---------------INÍCIO DA SEED DO LND---------------
## 1. ability 2. soap 3. album 4. resource
## 5. plate 6. fiber 7. immune 8. fringe [...]
## !!!VOCÊ DEVE ANOTAR ESTA SEED PARA PODER RESTAURAR A CARTEIRA!!!
```bash lnd successfully initialized!
``` O estado atual dos seus canais, no entanto, não pode ser recriado a partir
desta seed. Para isso, o Backup Estático de Canal armazenado em /data/
```bash lnd/data/chain/bitcoin/mainnet/channel.backup é atualizado para cada
``` abertura e fechamento de canal.
Há um guia dedicado para fazer um backup automático.
Retorne ao usuário admin.
[...] Nov 26 19:17:38 minibolt lnd[1004]: 2023-11-26 19:17:38.037 [INF] LNWL: Opened wallet Nov 26 19:17:38 minibolt lnd[1004]: 2023-11-26 19:17:38.204 [INF] CHRE: Primary chain is set to: bitcoin Nov 26 19:17:38 minibolt lnd[1004]: 2023-11-26 19:17:38.244 [INF] LNWL: Started listening for bitcoind block notifications via ZMQ on 127.0.0.1:
Nov 26 19:17:38 minibolt lnd[1004]: 2023-11-26 19:17:38.245 [INF] CHRE: Initializing bitcoind backed fee estimator in CONSERVATIVE mode Nov 26 19:17:38 minibolt lnd[1004]: 2023-11-26 19:17:38.244 [INF] LNWL: Started listening for bitcoind transaction notifications via ZMQ on 127.0.0.1:
Nov 26 19:17:40 minibolt lnd[1004]: 2023-11-26 19:17:40.576 [INF]
LNWL: The wallet has been unlocked without a time limit Nov 26 19:17:40 minibolt lnd[1004]: 2023-11-26 19:17:40.712 [INF] CHRE: LightningWallet opened Nov 26 19:17:40 minibolt lnd[1004]: 2023-11-26 19:17:40.722 [INF] SRVR: Proxying all network traffic via Tor (stream_isolation=true)! NOTE: Ensure the backend node is proxying over Tor as well Nov 26 19:17:40 minibolt lnd[1004]: 2023-11-26 19:17:40.723 [INF] TORC: Starting tor controller Nov 26 19:17:40 minibolt lnd[1004]: 2023-11-26 19:17:40.744 [INF] HSWC: Cleaning circuits from disk for closed channels Nov 26 19:17:40 minibolt lnd[1004]: 2023-11-26 19:17:40.744 [INF] HSWC: Finished cleaning: no closed channels found, no actions taken.
[...] exit
Verifique se o LND está em execução e as portas relacionadas estão ouvindo.
Saída esperada:
Pronto. Parabéns, você tem um node Lightning funcional, e agora precisa
aprender a gerir o seu node. Você pode fazê-lo diretamente da linha de
comando usando o lncli ou instalar um software que auxilia na gestão do node como o Thunderhub (https://docs.thunderhub.io/) e o LNDg (https://
```bash github.com/cryptosharks131/lndg#manual-installation
``` E-book: Lightning Network para Iniciantes - https://amzn.to/3y5M7dTPlay List Denny Torres - https://bit.ly/45mYjkIAula LNDG Diego Kolling - https://bit.ly/4dghstPara levar você ao próximo nível junte-se a comunidade de Node Runners:
LN - https://br-ln.comAnterior
```bash sudo ss -tulpn | grep LISTEN | grep lnd
``` tcp LISTEN 0 4096 127.0.0.1:10009 0.0.0.0:* users:(("lnd",pid=386562,fd=8)) tcp LISTEN 0 4096 127.0.0.1:8080 0.0.0.0:* users:(("lnd",pid=386562,fd=29)) tcp LISTEN 0 4096 127.0.0.1:9735 0.0.0.0:* users:(("lnd",pid=386562,fd=45)) tcp LISTEN 0 4096 *:9911 *:* users:(("lnd",pid=386562,fd=44))
# Upgrade
 Knots Próximo
## Instalação LNDg Atualizado há 4 dias
