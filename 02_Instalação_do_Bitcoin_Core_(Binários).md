2. # Instalação do Bitcoin Core

### Visão geral

A base de um nó Bitcoin soberano é um cliente Bitcoin totalmente validado. Ele
irá descarregar toda a blockchain e validar todas as transações que já
aconteceram. Após essa verificação inicial, o cliente poderá verificar a
validade de todas as transações futuras.

O seu cliente Bitcoin também atua como uma fonte de dados para outras
aplicações, como:

- Servidor Electrum (para uso com carteiras de software e hardware).
- Exploradores de blockchain.
- Clientes de Lightning Network.

Neste capítulo vamos instalar o **Bitcoin Core**, a implementação de referência
da rede Bitcoin.

> Atenção: o Bitcoin Core irá baixar toda a cadeia de blocos do Bitcoin e
> validá-la desde o bloco gênese (2009). Isso representa mais de 800.000 blocos
> e mais de 550 GB de dados. Dependendo do seu hardware e conexão, esse
> processo pode levar de alguns dias até mais de uma semana.

---

### 2.1. Download e verificação dos binários

Primeiro vamos baixar o binário oficial do Bitcoin Core e verificar sua
integridade (checksum) e autenticidade (assinaturas GPG e carimbo de
data/hora). Isso garante que você está instalando uma versão legítima, e não
um binário malicioso.

#### 2.1.1. Baixar os binários

1. Inicie sessão como `admin` e vá para um diretório temporário, que será
   apagado automaticamente após o reinício do sistema:

```bash
cd /tmp
```

2. Defina uma variável de ambiente com a versão desejada do Bitcoin Core
   (ajuste para a versão estável mais recente, se necessário):

```bash
VERSION=29.1
```

3. Baixe os binários e os arquivos de verificação mais recentes:

```bash
wget https://bitcoincore.org/bin/bitcoin-core-$VERSION/bitcoin-$VERSION-x86_64-linux-gnu.tar.gz
wget https://bitcoincore.org/bin/bitcoin-core-$VERSION/SHA256SUMS
wget https://bitcoincore.org/bin/bitcoin-core-$VERSION/SHA256SUMS.asc
```

#### 2.1.2. Verificar o checksum (integridade)

Verifique se a soma de verificação (checksum) informada no arquivo
`SHA256SUMS` corresponde ao arquivo que você baixou (ignore o aviso
`lines are improperly formatted`):

```bash
sha256sum --ignore-missing --check SHA256SUMS
```

Exemplo de saída esperada:

> bitcoin-29.0-x86_64-linux-gnu.tar.gz: OK

#### 2.1.3. Verificar as assinaturas GPG (autenticidade)

As versões do Bitcoin Core são assinadas por vários desenvolvedores, cada um
com a sua própria chave GPG. Vamos importar essas chaves e conferir as
assinaturas do arquivo de checksums.

1. Importar as chaves dos “builders” (Guix):

```bash
curl -s "https://api.github.com/repositories/355107265/contents/builder-keys" \
  | grep download_url \
  | grep -oE "https://[a-zA-Z0-9./-]+" \
  | while read url; do curl -s "$url" | gpg --import; done
```

Exemplo de saída esperada:

> gpg: key 17565732E08E5E41: 29 signatures not checked due to missing keys  
> gpg: /home/admin/.gnupg/trustdb.gpg: trustdb created  
> gpg: key 17565732E08E5E41: public key "Andrew Chow <andrew@achow101.com>" imported  
> gpg: Total number processed: 1  
> gpg: imported: 1  
> gpg: no ultimately trusted keys found

2. Verificar se o arquivo de checksums está assinado corretamente:

```bash
gpg --verify SHA256SUMS.asc
```

Confirme se pelo menos algumas das assinaturas exibem algo como:

> gpg: Good signature from ...  
> Primary key fingerprint: ...

#### 2.1.4. Verificar o carimbo de data/hora (OpenTimestamps)

Opcionalmente, você pode usar o site do OpenTimestamps para comprovar que o
arquivo `SHA256SUMS` já existia em determinada data (a data de lançamento).

1. No seu computador local, baixe:

   - o arquivo `SHA256SUMS` da versão;
   - o arquivo `SHA256SUMS.ots` (prova de timestamp).

2. Acesse o site do OpenTimestamps: https://opentimestamps.org.
3. Na seção “Stamp & Verify”, arraste o arquivo `SHA256SUMS.ots` para a caixa
   pontilhada.
4. Em seguida, arraste também o arquivo `SHA256SUMS` para a caixa indicada.
5. Se o carimbo de data/hora for válido, o site exibirá uma mensagem
   informando que o arquivo existia na data correspondente ao lançamento.

Quando estiver satisfeito com as verificações (checksum, assinatura e
timestamp), extraia os binários do Bitcoin Core:

```bash
tar -xvf bitcoin-$VERSION-x86_64-linux-gnu.tar.gz
```

Se quiser gerar um ficheiro bitcoin.conf completo (generate-a-full-bitcoin.conf-example-file), siga a secção extra adequada (generate-a-full-bitcoin.conf-example-file) e depois volte para continuar com a secção seguinte (binaries-installation)

Se pretender instalar a página de manual para bitcoin-cli, siga a página do manual para a secção extra da bitcoin-cli, e depois voltar para continuar com a secção seguinte (create-the-bitcoin-user-and-group).

### 2.2. Instalação dos binários

1. Instale o `bitcoind` e o `bitcoin-cli` em `/usr/local/bin`:

```bash
sudo install -m 0755 -o root -g root -t /usr/local/bin \
    bitcoin-$VERSION/bin/bitcoin-cli \
    bitcoin-$VERSION/bin/bitcoind
```

2. Verifique se a instalação foi bem-sucedida, exibindo a versão do daemon:

```bash
bitcoind --version
```

Exemplo de saída esperada:

> Bitcoin Core version v29.0.0  
> Copyright (C) 2009-2022 The Bitcoin Core developers

3. (Opcional) Limpe os arquivos usados na instalação para liberar espaço no
   diretório temporário:

```bash
sudo rm -r bitcoin-$VERSION \
    bitcoin-$VERSION-x86_64-linux-gnu.tar.gz \
    SHA256SUMS SHA256SUMS.asc SHA256SUMS.ots
```

Criar o utilizador e o grupo bitcoin

A aplicação Bitcoin Core será executada em segundo plano como um daemon e usará o utilizador separado "bitcoin" por razões de segurança. Este utilizador não tem direitos de administrador e não pode alterar a configuração do sistema.

    Criar o usuário e grupo bitcoin

Copiar

sudo adduser --gecos "" --disabled-password bitcoin

    Adicionar também o utilizador admin para o grupo "bitcoin"

Copiar

sudo adduser admin bitcoin

    Permitir que o utilizador bitcoin utilize a porta de controlo e configure o Tor diretamente, adicionando-o ao grupo "debian-tor"

Copiar

sudo adduser bitcoin debian-tor

Criar a Pasta de Dados

O Bitcoin Core utiliza por padrão a pasta .bitcoin na pasta home do usuário. Em vez de criar este diretório, nós criamos um diretório de dados no local de dados gerais /data e ligamos a ele.

    Criar a pasta de dados Bitcoin

Copiar

sudo mkdir /data/bitcoin

    Atribuir como proprietário ao utilizador `bitcoin

Copiar

sudo chown bitcoin:bitcoin /data/bitcoin

    Mudar para o utilizador bitcoin

Copiar

sudo su - bitcoin

    Crie a ligação simbólica .bitcoin que aponta para esse diretório

Copiar

ln -s /data/bitcoin /home/bitcoin/.bitcoin

    Verificar se a ligação simbólica foi criada corretamente

Copiar

ls -la

Resultado esperado:

total 32
drwxr-xr-x 3 bitcoin bitcoin 4096 Nov 7 19:33 .
drwxr-xr-x 4 root root 4096 Nov 7 19:32 ..
-rw------- 1 bitcoin bitcoin 135 Nov 7 19:33 .bash_history
-rw-r--r-- 1 bitcoin bitcoin 220 Nov 7 19:32 .bash_logout
-rw-r--r-- 1 bitcoin bitcoin 3523 Nov 7 19:32 .bashrc
lrwxrwxrwx 1 bitcoin bitcoin 13 Nov 7 19:32 .bitcoin -> /data/bitcoin
drwxr-xr-x 3 bitcoin bitcoin 4096 Nov 7 19:33 .local
-rw-r--r-- 1 bitcoin bitcoin 1670 Nov 7 19:32 .mkshrc
-rw-r--r-- 1 bitcoin bitcoin 807 Nov 7 19:32 .profile

Gerar As Credenciais de Acesso

Para que outros programas consultem o Bitcoin Core eles precisam das credenciais de acesso apropriadas. Para evitar armazenar o nome de usuário e a senha em um arquivo de configuração em texto simples, a senha é transformada em hash. Isso permite que o Bitcoin Core aceite uma senha, faça um hash e a compare com o hash armazenado, enquanto não é possível recuperar a senha original.

Outra opção para obter credenciais de acesso é através do arquivo .cookie no diretório de dados do Bitcoin. Este é criado automaticamente e pode ser lido por todos os utilizadores que sejam membros do grupo "bitcoin".

O Bitcoin Core fornece um programa Python simples para gerar a linha de configuração para o arquivo de configuração.

    Entrar na pasta bitcoin

Copiar

cd .bitcoin

    Descarregar o programa RPCAuth

Copiar

wget https://raw.githubusercontent.com/bitcoin/bitcoin/master/share/rpcauth/rpcauth.py

    Execute o script com o interpretador Python3, fornecendo o nome de utilizador (minibolt) e os seus argumentos "password [B]"

Todos os comandos introduzidos são guardados no histórico do bash. Mas nós não queremos que a senha seja armazenada onde qualquer um possa encontrá-la. Para isso, coloque um espaço no inicio do comando mostrado abaixo

Copiar

python3 rpcauth.py minibolt SuaPasswordB

Exemplo do resultado esperado:

> String to be appended to bitcoin.conf:
> rpcauth=minibolt:00d8682ce66c9ef3dd9d0c0a6516b10e$c31da4929b3d0e092ba1b2755834889f888445923ac8fd69d8eb73efe0699afa

    Copie a linha rpcauth, nós iremos precisar colar no arquivo de configuração do Bitcoin

Configuração

Agora, o arquivo de configuração bitcoind precisa ser criado. Também vamos definir as permissões de acesso adequadas.

    Ainda como o utilizador "bitcoin", cria o ficheiro bitcoin.conf

Copiar

nano /home/bitcoin/.bitcoin/bitcoin.conf

    Introduzir a configuração seguinte completa. Guardar e sair

Substitua toda a linha que começa com "rpcauth=..." pela string de conexão que você acabou de gerar

Copiar

# BRLNBolt: configuração do bitcoind

# /home/bitcoin/.bitcoin/bitcoin.conf

# Daemon Bitcoin

server=1
txindex=1

# Desativar a carteira integrada

disablewallet=1

# Registos adicionais

debug=tor
debug=i2p

# Atribuir ao ficheiro cookie permissão de leitura aos utilizadores

# do grupo Bitcoin

startupnotify=chmod g+r /home/bitcoin/.bitcoin/.cookie
rpccookieperms=group

# Desativar debug.log

nodebuglogfile=1

# Evita assumir que um bloco e os seus antepassados são válidos e,

# potencialmente, ignorar a verificação do seu script.

# Vamos definir este valor como 0, para verificar tudo.

assumevalid=0

# Ativar todos os filtros compactos

blockfilterindex=1

# Servir filtros de bloco compactos aos pares por BIP 157

peerblockfilters=1

# Atualizar o índice coinstats utilizado pelo RPC gettxoutsetinfo

coinstatsindex=1

# Network

listen=1

## P2P bind

bind=127.0.0.1
bind=127.0.0.1=onion

## Proxificar conexões de saída da clearnet usando o proxy Tor SOCKS5

proxy=127.0.0.1:9050

## I2P SAM proxy para contactar os pares I2P e aceitar ligações I2P

i2psam=127.0.0.1:7656

# Connections

rpcauth=<replace with your own auth line generated in the previous step>

# Optimizações da transferência inicial de blocos (defina o tamanho da

# dbcache em megabytes (4 a 16384, predefinição: 300) de acordo com a

# RAM disponível no seu dispositivo, recomendado: dbcache=1/2 x RAM

# disponível, por exemplo: 4GB RAM -> dbcache=2048)

# Lembre-se de comentar após o IBD (Initial Block Download)!

dbcache=2048
blocksonly=1

(Opcional) Se você marcou a seção Check IPv6 availability e você não tem IPv6 disponível, você pode descartar a rede IPv6 e o cjdns do Bitcoin Core adicionando as próximas linhas no final do arquivo de configuração:

Copiar

# Desativar redes IPv6 e cjdns

onlynet=onion
onlynet=i2p
onlynet=ipv4

-> Esta é uma configuração padrão. Verifique este arquivo Bitcoin Core sample bitcoind.conf com todas as opções possíveis ou gere um você mesmo seguindo a "seção extra")

    Definir permissões: apenas o utilizador bitcoin e membros do grupo bitcoin podem ler (necessário para o LND ler a linha "rpcauth")

Copiar

chmod 640 /home/bitcoin/.bitcoin/bitcoin.conf

    Sair da sessão do utilizador bitcoin e voltar ao utilizador admin

Copiar

exit

Criar o serviço systemd

O sistema precisa de executar o daemon bitcoin automaticamente em segundo plano. Nós usamos o systemd, um daemon que controla o processo de inicialização usando arquivos de configuração

    Criar a configuração do systemd

Copiar

sudo nano /etc/systemd/system/bitcoind.service

    Introduzir a configuração seguinte completa. Guardar e sair

Copiar

# MiniBolt: unidade systemd para bitcoind

# /etc/systemd/system/bitcoind.service

[Unit]
Description=Bitcoin Core Daemon
Requires=network-online.target
After=network-online.target

[Service]
ExecStart=/usr/local/bin/bitcoind -pid=/run/bitcoind/bitcoind.pid \
 -conf=/home/bitcoin/.bitcoin/bitcoin.conf \
 -datadir=/home/bitcoin/.bitcoin

# Gestão de processos

####################
Type=exec
NotifyAccess=all
PIDFile=/run/bitcoind/bitcoind.pid

Restart=on-failure
TimeoutStartSec=infinity
TimeoutStopSec=600

# Criação de diretórios e permissões

####################################
User=bitcoin
Group=bitcoin
RuntimeDirectory=bitcoind
RuntimeDirectoryMode=0710
UMask=0027

# Medidas de reforço

####################
PrivateTmp=true
ProtectSystem=full
NoNewPrivileges=true
PrivateDevices=true
MemoryDenyWriteExecute=true
SystemCallArchitectures=native

[Install]
WantedBy=multi-user.target

    Ativar o arranque automático (opcional)

Copiar

sudo systemctl enable bitcoind

    Preparar a monitorização "bitcoind" pelo diário systemd e verificar a saída de registo. Você pode sair do monitoramento a qualquer momento com Ctrl-C

Copiar

journalctl -fu bitcoind

Mantenha este terminal aberto, terá de voltar aqui no passo seguinte para monitorizar os registos
Executar

Para ficar de olho nos movimentos do software, inicie seu programa SSH (por exemplo, PuTTY) uma segunda vez, conecte-se ao nó MiniBolt e faça o login como admin

    Iniciar o serviço

Copiar

sudo systemctl start bitcoind

Exemplo da saída esperada no primeiro terminal com journalctl -fu bitcoind

> 2022-11-24T18:08:04Z Bitcoin Core version v24.0.1.0 (release build)
> 2022-11-24T18:08:04Z InitParameterInteraction: parameter interaction: -proxy set -> setting -upnp=0
> 2022-11-24T18:08:04Z InitParameterInteraction: parameter interaction: -proxy set -> setting -natpmp=0
> 2022-11-24T18:08:04Z InitParameterInteraction: parameter interaction: -proxy set -> setting -discover=0
> 2022-11-24T18:08:04Z Using the 'sse4(1way),sse41(4way),avx2(8way)' SHA256 implementation
> 2022-11-24T18:08:04Z Using RdRand as an additional entropy source
> 2022-11-24T18:08:04Z Default data directory /home/bitcoin/.bitcoin
> 2022-11-24T18:08:04Z Using data directory /home/bitcoin/.bitcoin
> 2022-11-24T18:08:04Z Config file: /home/bitcoin/.bitcoin/bitcoin.conf
> 2022-11-24T18:08:04Z Config file arg: blockfilterindex="1"
> 2022-11-24T18:08:04Z Config file arg: coinstatsindex="1"
> 2022-11-24T18:08:04Z Config file arg: i2pacceptincoming="1"
> 2022-11-24T18:08:04Z Config file arg: i2psam="127.0.0.1:7656"
> 2022-11-24T18:08:04Z Config file arg: listen="1"
> 2022-11-24T18:08:04Z Config file arg: listenonion="1"
> 2022-11-24T18:08:04Z Config file arg: peerblockfilters="1"
> 2022-11-24T18:08:04Z Config file arg: peerbloomfilters="1"
> 2022-11-24T18:08:04Z Config file arg: proxy="127.0.0.1:9050"
> 2022-11-24T18:08:04Z Config file arg: rpcauth=\*\*\*\*
> 2022-11-24T18:08:04Z Config file arg: server="1"
> 2022-11-24T18:08:04Z Config file arg: txindex="1"
> [...]
> 2022-11-24T18:09:04Z Synchronizing blockheaders, height: 4000 (~0.56%)
> [...]

Monitorize o ficheiro de registo durante alguns minutos para ver se funciona bem (se parar em "dnsseed thread exit", não faz mal)

    Vincule o diretório de dados do Bitcoin também a partir do diretório home do usuário admin. Isso permite que o usuário admin trabalhe com o bitcoind diretamente, por exemplo, usando o comando bitcoin-cli

Copiar

ln -s /data/bitcoin /home/admin/.bitcoin

    Esta ligação simbólica fica ativa apenas numa nova sessão de utilizador. Faça logout do SSH digitando o seguinte comando

Copiar

exit

    Inicie novamente a sessão como utilizador admin abrindo uma nova sessão SSH

    Verificar se a ligação simbólica foi criada corretamenteCopy

ls -la

Resultado esperado:

drwxr-xr-x 11 root root 4096 Oct 26 19:19 ..
-rw-rw-r-- 1 admin admin 12020 Nov 7 09:51 .bash_aliases
-rw------- 1 admin admin 51959 Nov 7 12:19 .bash_history
-rw-r--r-- 1 admin admin 220 Nov 7 20:25 .bash_logout
-rw-r--r-- 1 admin admin 3792 Nov 7 07:56 .bashrc
lrwxrwxrwx 1 admin admin 13 Nov 7 10:41 .bitcoin -> /data/bitcoin
-rw-r--r-- 1 admin admin 807 Nov 7 2023 .profile
drwx------ 2 admin admin 4096 Nov 7 2023 .ssh
-rw-r--r-- 1 admin admin 208 Nov 7 19:32 .wget-hsts
-rw------- 1 admin admin 116 Nov 7 19:41 .Xauthority

Nota de resolução de problemas: SOMENTE SE NÃO OBTEVE O RESULTADO ESPERADO (.bitcoin -> /data/bitcoin) e só tiver (.bitcoin), deve seguir os passos seguintes para resolver o problema:

    Eliminar a ligação simbólica criada com falha

Copiar

sudo rm -r .bitcoin

    Tente criar novamente a ligação simbólica

Copiar

ln -s /data/bitcoin /home/admin/.bitcoin

    Verifique se a ligação simbólica foi criada corretamente desta vez e se tem agora o resultado esperado: .bitcoin -> /data/bitcoin

Copiar

ls -la

    Espere alguns minutos até o Bitcoin Core iniciar e depois digite o próximo comando para obter seus endereços Tor e I2P. Anote-os, pois mais tarde você pode precisar deles

Copiar

bitcoin-cli getnetworkinfo | grep address.*onion && bitcoin-cli getnetworkinfo | grep address.*i2p

Exemplo do resultado esperado:

> "address": "vctk9tie5srguvz262xpyukkd7g4z2xxxy5xx5ccyg4f12fzop8hoiad.onion",
> "address": "sesehks6xyh31nyjldpyeckk3ttpanivqhrzhsoracwqjxtk3apgq.b32.i2p",

    Verificar a ativação correta das redes I2P e Tor

Copy

bitcoin-cli -netinfo

Exemplo do resultado esperado:

Bitcoin Core client v24.0.1 - server 70016/Satoshi:24.0.1/
ipv4 ipv6 onion i2p total block
in 0 0 25 2 27
out 7 0 2 1 10 2
total 7 0 27 3 37

Local addresses
xdtk6tie4srguvz566xpyukkd7m3z3vbby5xx5ccyg5f64fzop7hoiab.onion port 8333 score 4
etehks3xyh55nyjldjdeckk3nwpanivqhrzhsoracwqjxtk8apgk.b32.i2p port 0 score 4

    Certifique-se de que o bitcoind está a ouvir nos portos RPC e P2P predefinidas

Copiar

sudo ss -tulpn | grep LISTEN | grep bitcoind

Resultado esperado:

> tcp LISTEN 0 128 127.0.0.1:8332 0.0.0.0:_ users:(("bitcoind",pid=773834,fd=11))
> tcp LISTEN 0 4096 127.0.0.1:8333 0.0.0.0:_ users:(("bitcoind",pid=773834,fd=46))
> tcp LISTEN 0 4096 127.0.0.1:8334 0.0.0.0:_ users:(("bitcoind",pid=773834,fd=44))
> tcp LISTEN 0 128 [::1]:8332 [::]:_ users:(("bitcoind",pid=773834,fd=10))

    Atenção:

        Quando a "bitcoind" ainda estiver a iniciar, podes receber uma mensagem de erro como "a verificar blocos". Isso é normal, basta aguardar alguns minutos.

        Entre outras informações, é apresentado o "verificationprogress". Quando este valor atinge quase 1 ou próximo (0,999...), a cadeia de blocos está actualizada e totalmente validada.

O Bitcoin Core está sincronizando

Este processo é designado por IBD (Initial Block Download). Este processo pode demorar entre um dia e uma semana, dependendo sobretudo do desempenho do seu PC. É melhor esperar até que a sincronização esteja concluída antes de avançar
Ativar a mempool e reduzir a 'dbcache' após uma sincronização completa

Uma vez que o Bitcoin Core esteja totalmente sincronizado, nós podemos reduzir o tamanho do cache do banco de dados. Um cache maior acelera o download do bloco inicial, agora nós queremos reduzir o consumo de memória para permitir que o cliente Lightning e o servidor Electrum rodem em paralelo. Também queremos agora permitir que o nó ouça e retransmita transacções.

    Como usuário admin, edite o arquivo bitcoin.conf

Bitcoin Core irá então usar o tamanho de cache padrão de 450 MiB em vez de sua configuração de RAM. Se blocksonly=1 for deixado sem comentário ele irá prevenir o Electrum Server de receber dados de taxas RPC e não irá funcionar. Salve e saia

Copiar

sudo nano /home/bitcoin/.bitcoin/bitcoin.conf

    Comente as seguintes linhas (adicionando um # no início)

#dbcache=2048
#blocksonly=1
#assumevalid=0

    Reinicie o Bitcoin Core para que as configurações tenham efeito

Copiar

sudo systemctl restart bitcoind

OpenTimestamps client

Quando instalamos o Bitcoin Core, verificamos o carimbo de data e hora do arquivo de checksum usando o site OpenTimestamp. No futuro, você provavelmente precisará verificar mais carimbos de data/hora, ao instalar programas adicionais (por exemplo, LND) e ao atualizar programas existentes para uma versão mais recente. Em vez de depender de terceiros, seria preferível (e mais divertido) verificar os carimbos de data e hora usando seus dados de blockchain. Agora que o Bitcoin Core está rodando e sincronizado, podemos instalar o OpenTimestamp client para verificar localmente o timestamp do arquivo de checksums dos binários.

    Como utilizador admin, instalar as dependências

Copiar

sudo apt install python3-dev python3-pip python3-wheel

    Instalar o cliente OpenTimestamp

Copiar

sudo pip3 install opentimestamps-client

    Mostrar a versão do cliente OpenTimestamps para verificar se está corretamente instalado

Copiar

ots --version

Exemplo do resultado esperado:

Copiar

> v0.7.1

Para atualizar o cliente OpenTimestamps, basta executar sudo pip3 install --upgrade opentimestamps-client
Extras (optional)
Slow device mode

    Como utilizador admin edite o ficheiro bitcoin.conf

Copiar

sudo nano /home/bitcoin/.bitcoin/bitcoin.conf

    Adicione estas linhas ao final do ficheiro

Copiar

# Optimizações de dispositivos lentos

## Limitar o número máximo de ligações entre pares

maxconnections=40

## Tenta manter o tráfego de saída abaixo do objetivo definido por

## 24 horas

maxuploadtarget=5000

## Aumentar o número de threads para servir as chamadas RPC

## (predefinição: 4)

rpcthreads=128

## Aumentar a profundidade da fila de trabalho para servir as chamadas

## RPC (predefinição: 16)

rpcworkqueue=256

    Comente estas linhas

#coinstatsindex=1
#assumevalid=0

Upgrade

A última versão pode ser encontrada na página do GitHub do projeto Bitcoin Core. Leia sempre as RELEASE NOTES primeiro! Ao atualizar, pode haver mudanças significativas ou mudanças na estrutura de dados que precisam de atenção especial. Substitua o valor da variável de ambiente "VERSION=x.xx" para a versão mais recente se ela ainda não tiver sido alterada neste guia.

    Inicie sessão como utilizador admin e mude para o diretório temporário

Copiar

cd /tmp

    Definir uma variável de ambiente de versão temporária para a instalação

Copiar

VERSION=27.1

    Descarregar ficheiros binários, de soma de controlo, de assinatura e de carimbo de data/hora

Copiar

wget https://bitcoincore.org/bin/bitcoin-core-$VERSION/bitcoin-$VERSION-x86_64-linux-gnu.tar.gz

Copiar

wget https://bitcoincore.org/bin/bitcoin-core-$VERSION/SHA256SUMS

Copiar

wget https://bitcoincore.org/bin/bitcoin-core-$VERSION/SHA256SUMS.asc

Copiar

wget https://bitcoincore.org/bin/bitcoin-core-$VERSION/SHA256SUMS.ots

    Verificar a nova versão em relação às suas somas de controlo

Copiar

sha256sum --ignore-missing --check SHA256SUMS

Exemplo do resultado esperado:

> bitcoin-25.1-x86_64-linux-gnu.tar.gz: OK

    O próximo comando faz o download e importa automaticamente todas as assinaturas do repositório Bitcoin Core release attestations (Guix)

Copiar

curl -s "https://api.github.com/repositories/355107265/contents/builder-keys" | grep download_url | grep -oE "https://[a-zA-Z0-9./-]+" | while read url; do curl -s "$url" | gpg --import; done

Resultado esperado:

> gpg: key 17565732E08E5E41: 29 signatures not checked due to missing keys
> gpg: /home/admin/.gnupg/trustdb.gpg: trustdb created
> gpg: key 17565732E08E5E41: public key "Andrew Chow <andrew@achow101.com>" imported
> gpg: Total number processed: 1
> gpg: imported: 1
> gpg: no ultimately trusted keys found
> [...]

    Verifique se o ficheiro de somas de verificação é assinado criptograficamente pelas chaves de assinatura da versão. O seguinte comando imprime verificações de assinatura para cada uma das chaves públicas que assinaram as somas de verificação

Copiar

gpg --verify SHA256SUMS.asc

    Verificar se pelo menos algumas assinaturas apresentam o seguinte texto

> gpg: Good signature from ...
> Primary key fingerprint: ...

    Se completou o IBD (Initial Block Download), agora pode verificar o timestamp com o seu nó. Se o prompt mostrar -bash: ots: command not found, certifique-se que está a instalar o cliente OTS corretamente na secção opentimestamps-client.

Copiar

ots --no-cache verify SHA256SUMS.ots -f SHA256SUMS

O seguinte resultado é apenas um exemplo de uma das versões:

> Got 1 attestation(s) from https://btc.calendar.catallaxy.com
> Got 1 attestation(s) from https://finney.calendar.eternitywall.com
> Got 1 attestation(s) from https://bob.btc.calendar.opentimestamps.org
> Got 1 attestation(s) from https://alice.btc.calendar.opentimestamps.org
> Success! Bitcoin block 766964 attests existence as of 2022-12-11 UTC

Agora, basta verificar se a data do carimbo de data/hora está próxima da data release da versão que está a instalar

Se obtiver este resultado:

> Calendar https://btc.calendar.catallaxy.com: Pending confirmation in Bitcoin blockchain
> Calendar https://finney.calendar.eternitywall.com: Pending confirmation in Bitcoin blockchain
> Calendar https://bob.btc.calendar.opentimestamps.org: Pending confirmation in Bitcoin blockchain
> Calendar https://alice.btc.calendar.opentimestamps.org: Pending confirmation in Bitcoin blockchain

-> Isso significa que o carimbo de data/hora está pendente de confirmação no blockchain do Bitcoin. Podes saltar este passo ou esperar algumas horas/dias para fazer esta verificação. É seguro saltar este passo de verificação se tiveres seguido os passos anteriores e continuares para os passos seguintes

    Se estiver satisfeito com as verificações de soma de verificação, assinatura e carimbo de data/hora, extraia os binários do Bitcoin Core

Copiar

tar -xvf bitcoin-$VERSION-x86_64-linux-gnu.tar.gz

    Instalale

Copiar

sudo install -m 0755 -o root -g root -t /usr/local/bin bitcoin-$VERSION/bin/bitcoin-cli bitcoin-$VERSION/bin/bitcoind

    Verificar a nova versão

Copiar

bitcoin-cli --version

O seguinte resultado é apenas um exemplo de uma das versões:

> Bitcoin Core RPC client version v26.0.0
> Copyright (C) 2009-2022 The Bitcoin Core developers
> [...]

    (Opcional) Eliminar os ficheiros de instalação da pasta /tmp para estar pronto para a próxima atualização

Copiar

sudo rm -r bitcoin-$VERSION && sudo rm bitcoin-$VERSION-x86_64-linux-gnu.tar.gz && sudo rm SHA256SUMS && sudo rm SHA256SUMS.asc && sudo rm SHA256SUMS.ots

    Reinicie o Bitcoin Core para aplicar a nova versão

Copiar

sudo systemctl restart bitcoind

Desinstalar
Desinstalar o serviço

    Certifique-se de que tem sessão iniciada com o utilizador admin, pare o bitcoind

Copiar

sudo systemctl stop bitcoind

    Desativar o arranque automático (se ativado)

Copiar

sudo systemctl disable bitcoind

    Eliminar o serviço

Copiar

sudo rm /etc/systemd/system/bitcoind.service

Apagar Usuário e Grupo

    Eliminar o grupo de utilizadores bitcoin

Copiar

sudo gpasswd -d admin bitcoin; sudo gpasswd -d fulcrum bitcoin; sudo gpasswd -d lnd bitcoin; sudo gpasswd -d btcrpcexplorer bitcoin; sudo gpasswd -d btcpay bitcoin

    Apague o utilizador bitcoin. Não se preocupe com a saída userdel: bitcoin mail spool (/var/mail/bitcoin) not found, porque a desinstalação foi bem sucedida

Copiar

sudo userdel -rf bitcoin

    Eliminar o grupo bitcoin

Copiar

sudo groupdel bitcoin

Apagar a Pasta de Dados

    Eliminar o diretório bitcoin completo

Copiar

sudo rm -rf /data/bitcoin/

Desinstalar os binários

    Eliminar os binários instalados

Copiar

sudo rm /usr/local/bin/bitcoin-cli && sudo rm /usr/local/bin/bitcoind
