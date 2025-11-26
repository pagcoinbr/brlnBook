# BTCPay

Server (opcional)
O BTCPay Server é um gateway de pagamento Bitcoin gratuito, de código
aberto e auto-hospedado, o que significa que os programadores e os
auditores de segurança podem sempre inspecionar o código quanto à qualidade. Permite que indivíduos e empresas aceitem pagamentos em
Bitcoin online ou pessoalmente sem quaisquer taxas, oferecendo auto-soberania no processo.
Nível de Dificuldade: Difícil O BTCPay Server é um sistema de faturação auto-hospedado e
automatizado. No checkout, é apresentada ao cliente uma fatura que ele
paga a partir da sua carteira. O BTCPay Server segue o estado da fatura
através da cadeia de blocos e informa-o quando o pagamento tiver sido
liquidado para que possa cumprir a encomenda. Ele também cuida do
reembolso do pagamento e do gerenciamento de bitcoin, além de muitos outros recursos.
Para mais informações, consulte a documentação e fique atento às novidades no blogue

- Bitcoin Core

## • LND (opcional)

- NBXplorer
- Outros ◦.NET Core SDK
  ◦PostgreSQL Para executar o servidor BTCPay será necessário instalar o .NET Core SDK , PostgreSQL e NBXplorer
  Precisamos de definir definições no ficheiro de configuração do Bitcoin Core
- adiciona novas linhas se não estiverem presentes
- Com o usuário admin , edite o arquivo bitcoin.conf
- Adicione a seguinte linha à secção "# Ligações" . Guardar e sair
- Reiniciar o Bitcoin Core para aplicar as alterações

```bash
sudo nano /data/bitcoin/bitcoin.conf
```

# NBXplorer

Adicione a seguinte linha à secção "# Ligações" . Guardar e sair

```
whitelist=127.0.0.1
```

```bash
sudo systemctl restart bitcoind
```

- Configurar a Firewall para permitir pedidos HTTP de entrada Resultado esperado
- Vamos utilizar o modo de instalação com script. Descarregar o script
- Antes de executar este script, terá de conceder permissão para que este script seja executado como um executável
- Definir a versão da variável de ambiente
- Instalar o SDK do .NET Core Example of expected output

````bash sudo ufw allow 23000/tcp comment 'permitir o servidor BTCPay a
``` partir de qualquer lugar' Rule added Rule added (v6)
```bash wget https://dotnet.microsoft.com/download/dotnet/scripts/v1/``` dotnet-install.sh
```bash chmod +x ./dotnet-install.sh
````

## VERSION=8.

./dotnet-install.sh --channel $VERSION

- Adicionar caminho para o executável dotnet
  Para melhorar a sua privacidade, desativar a telemetria do SDK do .NET Core
- Verificar se o .NET SDK está corretamente instalado dotnet-install: Attempting to download using aka.ms link sdk-6.0.417-linux-x64.tar.gz dotnet-install: Remote file https://dotnetcli.azureedge.net/dotnet/Sdk/6.0.417/dotnet-sdk-6.0.417-linux-x64.tar.gz size is 186250370 bytes.
  dotnet-install: Extracting zip from https:// dotnetcli.azureedge.net/dotnet/Sdk/6.0.417/dotnet-sdk-6.0.417-linux-x64.tar.gz dotnet-install: Downloaded file size is 186250370 bytes.
  dotnet-install: The remote and local file sizes are equal.
  dotnet-install: Installed version is 6.0.
  dotnet-install: Adding to current process PATH: `/home/

## btcpay/.dotnet`. Note: This change will be visible only when sourcing script.

dotnet-install: Note that the script does not resolve dependencies during installation.
dotnet-install: To check the list of dependencies, go to operating system and check the "Dependencies" section.
dotnet-install: Installation finished successfully.

````bash
echo 'export DOTNET_ROOT=$HOME/.dotnet' >>~/.bashrc
echo 'export PATH=$PATH:$HOME/.dotnet:$HOME/.dotnet/tools' >>~/.bashrc
echo 'export DOTNET_CLI_TELEMETRY_OPTOUT=1' >>~/.bashrc
source ~/.bashrc
``` do resultado esperado:
- Eliminar o script de instalação
- Com o utilizador admin , verifique se já instalou o PostgreSQL do resultado esperado:
Se o PostgreSQL não estiver instalado (saída: Command 'psql' not found), siga este guia PostgreSQL para instalá-lo Criar bases de dados PostgreSQL
- Crie uma nova base de dados para o NBXplorer com o utilizador postgres e atribua o utilizador admin como proprietário
- Criar uma nova base de dados para o servidor BTCPay com o utilizador postgres e atribuir o utilizador admin como proprietário dotnet --version > 6.0.
rm dotnet-install.sh psql -V > psql (PostgreSQL) 16.3 (Ubuntu 16.3-1.pgdg22.04+1)
```bash sudo -u postgres psql -c "CREATE DATABASE nbxplorer TEMPLATE
``` 'template0' LC_CTYPE 'C' LC_COLLATE 'C' ENCODING 'UTF8' OWNER admin;" NBXplorer
é um rastreador UTXO minimalista para carteiras HD, usado pelo servidor BTCPay
- Crie um diretório src e entre na pasta
- Definir a versão da variável de ambiente
- Descarregue o código-fonte do NBXplorer e entre na pasta Exemplo de resultados esperados
```bash sudo -u postgres psql -c "CREATE DATABASE btcpay TEMPLATE
``` 'template0' LC_CTYPE 'C' LC_COLLATE 'C' ENCODING 'UTF8' OWNER admin;"
```bash mkdir src && cd src
````

## VERSION=2.5.

`bash git clone --branch v$VERSION https://github.com/dgarage/` NBXplorer.git

- Modificar o script de execução do NBXplorer
- Comentar a linha existente Cloning into 'btcpayserver'...
  remote: Enumerating objects: 75078, done.
  remote: Counting objects: 100% (2765/2765), done.
  remote: Compressing objects: 100% (1249/1249), done.
  remote: Total 75078 (delta 1834), reused 2203 (delta 1485),
  pack-reused Receiving objects: 100% (75078/75078), 51.55 MiB | 4.86 MiB/s, done.
  Resolving deltas: 100% (58704/58704), done.
  Note: switching to 'a921504bcf619c5e845813b8f994b39147694a97'.
  You are in 'detached HEAD' state. You can look around, make
  experimental changes and commit them, and you can discard any commits you make in this
  state without impacting any branches by switching back to a branch.
  If you want to create a new branch to retain commits you create, you may
  do so (now or later) by using -c with the switch command.
  Example:

````bash git switch -c <new-branch-name>
``` Or undo this operation with:
```bash git switch -
``` Turn off this advice by setting config variable advice.detachedHead to false
```bash cd NBXplorer
````

```bash nano run.sh

```

- Acrescentar a linha seguinte. Guardar e sair
- Modificar o script de compilação do NBXplorer
- Comentar a linha seguinte
- Acrescentar a linha seguinte. Guardar e sair
- Criar o NBXplorer do resultado esperado
  #dotnet run --no-launch-profile --no-build -c Release --project "NBXplorer/NBXplorer.csproj" -- $@ /home/btcpay/.dotnet/dotnet run --no-launch-profile --no-build -c Release --project "NBXplorer/NBXplorer.csproj" -- $@

```bash nano build.sh

```

#dotnet build -c Release NBXplorer/NBXplorer.csproj /home/btcpay/.dotnet/dotnet build -c Release NBXplorer/ NBXplorer.csproj ./build.sh

- Verificar a instalação correta do resultado esperado:
  Welcome to .NET 8.0!
  SDK Version: 8.0.
  Installed an ASP.NET Core HTTPS development certificate.
  To trust the certificate, view the instructions: https:// aka.ms/dotnet-https-linux Write your first app: https://aka.ms/dotnet-hello-worldFind out what's new: https://aka.ms/dotnet-whats-newExplore documentation: https://aka.ms/dotnet-docsReport issues and find source on GitHub: https://github.com/dotnet/core Use 'dotnet --help' to see available commands or visit:
  MSBuild version 17.8.3+195e7f5a3 for .NET Determining projects to restore...
  Restored /home/btcpay/src/NBXplorer/NBXplorer.Client/ NBXplorer.Client.csproj (in 30.33 sec).
  Restored /home/btcpay/src/NBXplorer/NBXplorer/ NBXplorer.csproj (in 30.35 sec).
  NBXplorer.Client -> /home/btcpay/src/NBXplorer/ NBXplorer.Client/bin/Release/netstandard2.1/ NBXplorer.Client.dll NBXplorer -> /home/btcpay/src/NBXplorer/NBXplorer/bin/ Release/net8.0/NBXplorer.dll Build succeeded.
  0 Warning(s)
  0 Error(s)
  Time Elapsed 00:00:41.
  head -n 6 /home/btcpay/src/NBXplorer/NBXplorer/NBXplorer.csproj | grep Version
- Criar a pasta de dados e navegar até ela
- Criar um novo ficheiro de configuração
- Acrescentar todas as linhas seguintes. Guardar e sair
- Criar o ficheiro de serviço
- Colar a seguinte configuração. Guardar e sair > <Version>2.4.3</Version>

```bash mkdir -p ~/.nbxplorer/Main

```

```bash cd ~/.nbxplorer/Main

```

```bash nano settings.config

```

# MiniBolt: configuração do nbxplorer

# /home/btcpay/.nbxplorer/Main/settings.config

# Ligação

Bitcoind btc.rpc.cookiefile=/data/bitcoin/.cookie

# Base

de dados postgres=User ID=admin;Password=admin;Host=localhost;Port=5432;Database=nbxplore

```bash sudo nano /etc/systemd/system/nbxplorer.service

```

- Ativar o arranque automático
- Prepare a monitorização do nbxplorer através do diário do systemd e
  verifique a saída do registo. Você pode sair do monitoramento a qualquer momento com Ctrl-C

# BRLN

Bolt: unidade systemd para o NBXplorer

# /etc/systemd/system/nbxplorer.service [Unit] Description=NBXplorer Requires=bitcoind.service postgresql.service After=bitcoind.service postgresql.service [Service] WorkingDirectory=/home/btcpay/src/NBXplorer ExecStart=/home/btcpay/src/NBXplorer/run.sh User=btcpay Group=btcpay

# Gestão

de processos
##################### Type=simple TimeoutSec=

# Medidas

de reforço
#################### PrivateTmp=true ProtectSystem=full NoNewPrivileges=true PrivateDevices=true [Install] WantedBy=multi-user.target

````bash sudo systemctl enable nbxplorer
``` journalctl -fu nbxplorer Mantenha terá de voltar aqui no passo seguinte para monitorizar os registos
Para ficar de olho nos movimentos do software, inicie seu programa SSH
(por exemplo, PuTTY) uma segunda vez, conecte-se ao nó MiniBolt e faça login como "admin"
- Iniciar o serviço nbxplorer .
da saída esperada no primeiro terminal com journalctl -fu nbxplorer
```bash sudo systemctl start nbxplorer
``` Jul 05 17:50:20 minibolt systemd[1]: Started NBXplorer daemon.
Jul 05 17:50:21 minibolt run.sh[2808966]: info: Configuration:
Data Directory: /home/btcpay/.nbxplorer/Main Jul 05 17:50:21 minibolt run.sh[2808966]: info: Configuration:
Configuration File: /home/btcpay/.nbxplorer/Main/ settings.config Jul 05 17:50:21 minibolt run.sh[2808966]: info: Configuration:
Network: Mainnet Jul 05 17:50:21 minibolt run.sh[2808966]: info: Configuration:
Supported chains: BTC Jul 05 17:50:21 minibolt run.sh[2808966]: info: Configuration:
DBCache: 50 MB Jul 05 17:50:21 minibolt run.sh[2808966]: info: Configuration:
Network: Mainnet Jul 05 17:50:21 minibolt run.sh[2808966]: info: Configuration:
Supported chains: BTC Jul 05 17:50:21 minibolt run.sh[2808966]: info: Configuration:
DBCache: 50 MB Jul 05 17:50:21 minibolt run.sh[2808966]: info:
NBXplorer.DatabaseSetup: Postgres services activated Jul 05 17:50:21 minibolt run.sh[2808966]: info:
NBXplorer.DatabaseSetup: Execute script 001.Migrations...
Jul 05 17:50:21 minibolt run.sh[2808966]: info:
NBXplorer.DatabaseSetup: Execute script 002.Model...
Jul 05 17:50:22 minibolt run.sh[2808966]: info:
NBXplorer.DatabaseSetup: Execute script 003.Legacy...
Jul 05 17:50:22 minibolt run.sh[2808966]: info:
NBXplorer.DatabaseSetup: Execute script 004.Fixup...
Jul 05 17:50:22 minibolt run.sh[2808966]: info:
NBXplorer.DatabaseSetup: Execute script 005.ToBTCFix...
Jul 05 17:50:22 minibolt run.sh[2808966]: info:
NBXplorer.DatabaseSetup: Execute script 006.GetWalletsRecent2...
Jul 05 17:50:22 minibolt run.sh[2808966]: info:
NBXplorer.DatabaseSetup: Execute script 007.FasterSaveMatches...
Jul 05 17:50:22 minibolt run.sh[2808966]: info:
NBXplorer.DatabaseSetup: Execute script 008.FasterGetUnused...
Jul 05 17:50:22 minibolt run.sh[2808966]: info:
NBXplorer.DatabaseSetup: Execute script 009.FasterGetUnused2...
Jul 05 17:50:22 minibolt run.sh[2808966]: info:
NBXplorer.DatabaseSetup: Execute script 010.ChangeEventsIdType...
Jul 05 17:50:22 minibolt run.sh[2808966]: info:
NBXplorer.DatabaseSetup: Execute script 011.FixGetWalletsRecent...
Jul 05 17:50:22 minibolt run.sh[2808966]: info:
NBXplorer.DatabaseSetup: Execute script 012.PerfFixGetWalletsRecent...
Jul 05 17:50:22 minibolt run.sh[2808966]: info:
NBXplorer.DatabaseSetup: Execute script 013.FixTrackedTransactions...
Jul 05 17:50:22 minibolt run.sh[2808966]: info:
NBXplorer.DatabaseSetup: Execute script 014.FixAddressReuse...
Jul 05 17:50:22 minibolt run.sh[2808966]: info:
NBXplorer.DatabaseSetup: Execute script 015.AvoidWAL...
Jul 05 17:50:22 minibolt run.sh[2808966]: info:
NBXplorer.Indexer.BTC: TCP Connection succeed, handshaking...
Jul 05 17:50:22 minibolt run.sh[2808966]: info:
NBXplorer.Indexer.BTC: Handshaked Jul 05 17:50:22 minibolt run.sh[2808966]: info:
NBXplorer.Indexer.BTC: Testing RPC connection to http:// localhost:8332/ Jul 05 17:50:22 minibolt run.sh[2808966]: Hosting environment:
Production Jul 05 17:50:22 minibolt run.sh[2808966]: Content root path: / home/btcpay/src/NBXplorer/NBXplorer/bin/Release/net6.0/ Jul 05 17:50:22 minibolt run.sh[2808966]: Now listening on:
Jul 05 17:50:22 minibolt run.sh[2808966]: Application started.
Press Ctrl+C to shut down.
Jul 05 17:50:22 minibolt run.sh[2808966]: info:
NBXplorer.Indexer.BTC: RPC connection successful Jul 05 17:50:22 minibolt run.sh[2808966]: info:
NBXplorer.Indexer.BTC: Full node version detected:
Jul 05 17:50:22 minibolt run.sh[2808966]: info:
NBXplorer.Indexer.BTC: Has txindex support Jul 05 17:50:22 minibolt run.sh[2808966]: warn:
NBXplorer.Indexer.BTC: BTC: Your NBXplorer server is not whitelisted by your node, you should add "whitelist=127.0.0.1"
to the configuration file of your node. (Or use whitebind)
Jul 05 17:50:22 minibolt run.sh[2808966]: info:
NBXplorer.Events: BTC: Node state changed: NotStarted => NBXplorerSynching Jul 05 17:50:22 minibolt run.sh[2808966]: info:
NBXplorer.Indexer.BTC: Current Index Progress not found, start syncing from the header's chain tip (At height: 797318)
Jul 05 17:50:22 minibolt run.sh[2808966]: info:
NBXplorer.Events: BTC: Node state changed: NBXplorerSynching => Ready Jul 05 17:50:23 minibolt run.sh[2808966]: info:
NBXplorer.Events: BTC: New block 00000000000000000001415583131d3c1da985497830abcf638413226892d4a d (797318)
[..]
- Certifique-se de que o NBXplorer esteja em execução e escutando no porto padrão Resultado esperado:
Tem agora o NBxplorer a funcionar e preparado para que o servidor
## BTCpay o utilize
- Vá para a pasta src
- Definir a variável versão do ambiente
- Clonar o repositório oficial do GitHub do servidor BTCPay Exemplo de resultados esperados
```bash sudo ss -tulpn | grep LISTEN | grep NBXplorer
``` > tcp LISTEN 0 512 127.0.0.1:24444 0.0.0.0:* users:
(("NBXplorer",pid=2808966,fd=176))
```bash cd src
````

## VERSION=1.13.

`bash git clone --branch v$VERSION https://github.com/btcpayserver/`

## btcpayserver

- Vá para a pasta btcpayserver
- Modificar o script de execução do servidor BTCPay
- Comentar a linha seguinte Cloning into 'btcpayserver'...
  remote: Enumerating objects: 75078, done.
  remote: Counting objects: 100% (2765/2765), done.
  remote: Compressing objects: 100% (1249/1249), done.
  remote: Total 75078 (delta 1834), reused 2203 (delta 1485),
  pack-reused Receiving objects: 100% (75078/75078), 51.55 MiB | 4.86 MiB/s, done.
  Resolving deltas: 100% (58704/58704), done.
  Note: switching to 'a921504bcf619c5e845813b8f994b39147694a97'.
  You are in 'detached HEAD' state. You can look around, make
  experimental changes and commit them, and you can discard any commits you make in this
  state without impacting any branches by switching back to a branch.
  If you want to create a new branch to retain commits you create, you may
  do so (now or later) by using -c with the switch command.
  Example:

````bash git switch -c <new-branch-name>
``` Or undo this operation with:
```bash git switch -
``` Turn off this advice by setting config variable advice.detachedHead to false
```bash cd btcpayserver
````

```bash nano run.sh

```

- Acrescentar a linha seguinte. Guardar e sair
- Modificar o script de construção do servidor BTCPay
- Comentar a linha seguinte
- Acrescentar a linha seguinte. Guardar e sair
- Construir servidor BTCPay Exemplo de resultados esperados
  #dotnet "BTCPayServer.dll" $@ /home/btcpay/.dotnet/dotnet "BTCPayServer.dll" $@

```bash nano build.sh

```

#dotnet publish --no-cache -o BTCPayServer/bin/Release/publish/ -c Release BTCPayServer/BTCPayServer.csproj /home/btcpay/.dotnet/dotnet publish --no-cache -o BTCPayServer/ bin/Release/publish/ -c Release BTCPayServer/BTCPayServer.csproj ./build.sh

- Verificar a instalação correta MSBuild version 17.3.2+561848881 for .NET Determining projects to restore...
  Restored /home/btcpay/src/btcpayserver/BTCPayServer.Rating/

## BTCPayServer.Rating.csproj (in 32.66 sec).

Restored /home/btcpay/src/btcpayserver/BTCPayServer.Data/

## BTCPayServer.Data.csproj (in 1.41 sec).

Restored /home/btcpay/src/btcpayserver/BTCPayServer.Common/

## BTCPayServer.Common.csproj (in 392 ms).

Restored /home/btcpay/src/btcpayserver/BTCPayServer.Client/

## BTCPayServer.Client.csproj (in 1.1 sec).

Restored /home/btcpay/src/btcpayserver/

## BTCPayServer.Abstractions/BTCPayServer.Abstractions.csproj (in 8 ms).

Restored /home/btcpay/src/btcpayserver/BTCPayServer/

## BTCPayServer.csproj (in 36.6 sec).

## BTCPayServer.Common -> /home/btcpay/src/btcpayserver/

## BTCPayServer.Common/bin/Release/net6.0/BTCPayServer.Common.dll

## BTCPayServer.Client -> /home/btcpay/src/btcpayserver/

## BTCPayServer.Client/bin/Release/netstandard2.1/

## BTCPayServer.Client.dll

## BTCPayServer.Rating -> /home/btcpay/src/btcpayserver/

## BTCPayServer.Rating/bin/Release/net6.0/BTCPayServer.Rating.dll

## BTCPayServer.Abstractions -> /home/btcpay/src/btcpayserver/

## BTCPayServer.Abstractions/bin/Release/net6.0/

## BTCPayServer.Abstractions.dll

## BTCPayServer.Data -> /home/btcpay/src/btcpayserver/

## BTCPayServer.Data/bin/Release/net6.0/BTCPayServer.Data.dll /home/btcpay/src/btcpayserver/BTCPayServer/Services/ Cheater.cs(37,35): warning CS1998: This async method lacks 'await' operators and will run synchronously. Consider using

the 'await' operator to await non-blocking API calls, or 'await
Task.Run(...)' to do CPU-bound work on a background thread. [/ home/btcpay/src/btcpayserver/BTCPayServer/BTCPayServer.csproj]

## BTCPayServer -> /home/btcpay/src/btcpayserver/BTCPayServer/ bin/Release/net6.0/BTCPayServer.dll

## BTCPayServer -> /home/btcpay/src/btcpayserver/BTCPayServer/ bin/Release/publish/ head -n 3 /home/btcpay/src/btcpayserver/Build/Version.csproj | grep Version do resultado esperado:

- Criar a pasta de dados e introduzi-la
- Criar um novo ficheiro de configuração
- Acrescentar as seguintes linhas completas
  Se quiser ligar também o seu nó LND Lightning à BTCpay, vá à secção opcional Ligar ao seu nó interno LND
- Criar o ficheiro de serviço > <Version>1.12.0</Version>

```bash mkdir -p ~/.btcpayserver/Main && cd ~/.btcpayserver/Main

```

```bash nano settings.config

```

# MiniBolt: Configuração do servidor btcpayserver

# /home/btcpay/.btcpayserver/Main/settings.config

# Definições

do servidor bind=0.0.0.

# Base

de dados

## NBXplorer explorer.postgres=User ID=admin;Password=admin;Host=localhost;Port=5432;Database=nbxplore

## BTCpay server postgres=User ID=admin;Password=admin;Host=localhost;Port=5432;Database=btcpay;

- Colar a seguinte configuração. Guardar e sair
- Ativar o arranque automático
- Prepare a monitorização do btcpay com o diário do systemd e verifique
  a saída do registo. Você pode sair da monitorização a qualquer momento com Ctrl-C Mantenha terá de voltar aqui no passo seguinte para monitorizar os registos

```bash sudo nano /etc/systemd/system/btcpay.service

```

# BRLN

Bolt: unidade systemd para o servidor BTCpay

# /etc/systemd/system/btcpay.service [Unit] Description=BTCPay Server Requires=nbxplorer.service postgresql.service lnd.service After=nbxplorer.service postgresql.service lnd.service [Service] WorkingDirectory=/home/btcpay/src/btcpayserver ExecStart=/home/btcpay/src/btcpayserver/run.sh User=btcpay Group=btcpay

# Gestão

de processos
##################### Type=simple TimeoutSec= [Install] WantedBy=multi-user.target

````bash sudo systemctl enable btcpay
``` journalctl -fu btcpay
Para ficar de olho nos movimentos do software, inicie seu programa SSH
(por exemplo, PuTTY) uma segunda vez, conecte-se ao nó MiniBolt e faça o login como admin
of expected output on the first terminal with journalctl -fu
## btcpay
```bash sudo systemctl start btcpay
``` Jul 05 18:01:08 minibolt run.sh[2810276]: info: Configuration:
Data Directory: /home/btcpay/.btcpayserver/Main Jul 05 18:01:08 minibolt run.sh[2810276]: info: Configuration:
Configuration File: /home/btcpay/.btcpayserver/Main/ settings.config Jul 05 18:01:09 minibolt run.sh[2810276]: info:
## BTCPayServer.Plugins.PluginManager: Loading plugins from /home/
## btcpay/.btcpayserver/Plugins Jul 05 18:01:09 minibolt run.sh[2810276]: info:
## BTCPayServer.Plugins.PluginManager: Adding and executing plugin
## BTCPayServer - 1.10.
Jul 05 18:01:09 minibolt run.sh[2810276]: info:
## BTCPayServer.Plugins.PluginManager: Adding and executing plugin
## BTCPayServer.Plugins.Shopify - 1.10.
Jul 05 18:01:09 minibolt run.sh[2810276]: info:
## BTCPayServer.Plugins.PluginManager: Adding and executing plugin
## BTCPayServer.Plugins.PointOfSale - 1.10.
Jul 05 18:01:09 minibolt run.sh[2810276]: info:
## BTCPayServer.Plugins.PluginManager: Adding and executing plugin
## BTCPayServer.Plugins.PayButton - 1.10.
Jul 05 18:01:09 minibolt run.sh[2810276]: info:
## BTCPayServer.Plugins.PluginManager: Adding and executing plugin
## BTCPayServer.Plugins.NFC - 1.10.
Jul 05 18:01:09 minibolt run.sh[2810276]: info:
## BTCPayServer.Plugins.PluginManager: Adding and executing plugin
## BTCPayServer.Plugins.Crowdfund - 1.10.
Jul 05 18:01:09 minibolt run.sh[2810276]: info: Configuration:
Supported chains: BTC Jul 05 18:01:09 minibolt run.sh[2810276]: info: Configuration:
BTC: Explorer url is http://127.0.0.1:24444/ Jul 05 18:01:09 minibolt run.sh[2810276]: info: Configuration:
BTC: Cookie file is /home/btcpay/.nbxplorer/Main/.cookie Jul 05 18:01:09 minibolt run.sh[2810276]: info: Configuration:
Network: Mainnet Jul 05 18:01:13 minibolt run.sh[2810276]: info: Configuration:
Root Path: / Jul 05 18:01:14 minibolt run.sh[2810276]: info: PayServer:
Checking if any payment arrived on lightning while the server was offline...
Jul 05 18:01:14 minibolt run.sh[2810276]: info: PayServer:
Processing lightning payments...
Jul 05 18:01:14 minibolt run.sh[2810276]: info: PayServer:
Starting listening NBXplorer (BTC)
Jul 05 18:01:14 minibolt run.sh[2810276]: info: PayServer:
Start watching invoices Jul 05 18:01:14 minibolt run.sh[2810276]: info: PayServer:
Starting payment request expiration watcher Starting payment request expiration watcher Jul 05 18:01:14 minibolt run.sh[2810276]: info: PayServer:
pending payment requests being checked since last run Jul 05 18:01:14 minibolt run.sh[2810276]: info: Configuration:
Now listening on: http://127.0.0.1:
Jul 05 18:01:14 minibolt run.sh[2810276]: info: PayServer:
BTC: Checking if any pending invoice got paid while offline...
Jul 05 18:01:14 minibolt run.sh[2810276]: info: PayServer:
BTC: 0 payments happened while offline Jul 05 18:01:14 minibolt run.sh[2810276]: info: PayServer:
Connected to WebSocket of NBXplorer (BTC)
[...] Certifique-se de que o servidor BTCPay está a funcionar e a ouvir no porto padrão Resultado esperado:
Agora aponte seu navegador, "http://minibolt.local:23000" (ou o endereço IP do seu nó) como "http://192.168.x.x:23000"
Pode agora criar a primeira conta para aceder ao painel de controlo
utilizando um e-mail real (recomendado) ou um e-mail fictício + palavra-passe Parabéns! Agora tem o fantástico processador de pagamentos BTCPay Server a funcionar
```bash sudo ss -tulpn | grep LISTEN | grep
``` > tcp LISTEN 0 512 0.0.0.0:23000 0.0.0.0:* users:
(("dotnet",pid=2811744,fd=320))
- Configure o LND para permitir o LND REST de qualquer lugar editando o arquivo lnd.conf .
- Adicione a linha seguinte na secção [Opções da aplicação] . Guardar e sair
- Reiniciar o LND para aplicar as alterações
- Certifique-se de que o porto REST agora está vinculada ao host 0.0.0.0 em vez de 127.0.0.
Resultado esperado:
- Parar o servidor BTCPay antes de fazer alterações
- Editar o ficheiro settings.config .
```bash sudo nano /data/lnd/lnd.conf
````

# Especificar

todas as interfaces ipv4 para escutar as ligações

## REST restlisten=0.0.0.0:

```bash sudo systemctl restart lnd

```

````bash sudo ss -tulpn | grep LISTEN | grep lnd | grep
``` > tcp LISTEN 0 4096 0.0.0.0:8080 0.0.0.0:* users:(("lnd",pid=774047,fd=32))
```bash sudo systemctl stop btcpay
````

- Adicionar o conteúdo seguinte no final do ficheiro. Guardar e sair
- Modifique as próximas linhas do arquivo de serviço systemd seguindo a seção [create-btcpay-server-systemd-service], adicionando a dependência lnd.service
- Recarregar o daemon do systemd
- Iniciar o servidor BTCPay novamente
  Monitorize os registos com journalctl -fu btcpay para garantir que tudo está a correr bem A atualização para uma nova versão do BTCPay Server ou NBXplorer deve ser simples.

```bash nano .btcpayserver/Main/settings.config

```

# Ligação

do nó interno da Lightning BTC.lightning=type=lnd-rest;server=https://127.0.0.1:8080/;macaroonfilepath=/data/lnd/data/chain/bitcoin/mainnet/admin.macaroon;allowinsecure=true Requires=nbxplorer.service lnd.service After=nbxplorer.service lnd.service

```bash sudo systemctl daemon-reload

```

```bash sudo systemctl start btcpay

```

- Parar o servidor BTCPay e o NBXplorer
- Vamos utilizar o modo de instalação com script. Descarregar o script
- Antes de executar este script, terá de conceder permissão para que este script seja executado como um executável
- Defina a nova variável de ambiente VERSION , por exemplo, 6.0  8.
- Instalar o SDK do .NET Core Exemplo de resultados esperados

```bash sudo systemctl stop btcpay && sudo systemctl stop nbxplorer

```

`bash wget https://dotnet.microsoft.com/download/dotnet/scripts/v1/` dotnet-install.sh

```bash chmod +x ./dotnet-install.sh

```

## VERSION=8.

./dotnet-install.sh --channel $VERSION
Se não o tiver feito antes, para melhorar a sua privacidade, desactive a telemetria do SDK do .NET Core

- Aplicar alterações
- Verificar se a nova versão do .NET SDK foi corretamente instalada do resultado esperado:
- Eliminar o script de instalação dotnet-install: Attempting to download using aka.ms link https:// dotnetcli.azureedge.net/dotnet/Sdk/6.0.417/dotnet-sdk-6.0.417-linux-x64.tar.gz dotnet-install: Remote file https://dotnetcli.azureedge.net/dotnet/Sdk/6.0.417/dotnet-sdk-6.0.417-linux-x64.tar.gz size is 186250370 bytes.
  dotnet-install: Extracting zip from https:// dotnetcli.azureedge.net/dotnet/Sdk/6.0.417/dotnet-sdk-6.0.417-linux-x64.tar.gz dotnet-install: Downloaded file size is 186250370 bytes.
  dotnet-install: The remote and local file sizes are equal.
  dotnet-install: Installed version is 6.0.
  dotnet-install: Adding to current process PATH: `/home/

## btcpay/.dotnet`. Note: This change will be visible only when sourcing script.

dotnet-install: Note that the script does not resolve dependencies during installation.
dotnet-install: To check the list of dependencies, go to https:// learn.microsoft.com/dotnet/core/install, select your operating system and check the "Dependencies" section.
dotnet-install: Installation finished successfully.
echo 'export DOTNET_CLI_TELEMETRY_OPTOUT=1' >> ~/.bashrc source ~/.bashrc dotnet --version > 6.0.

- Com o utilizador admin , pare o servidor BTCPay e o NBXplorer
- Entre na pasta `src/nbxplorer
- Definir a versão da variável de ambiente
- Obter as alterações da última etiqueta desejada do resultado esperado:
  rm dotnet-install.sh

```bash sudo systemctl stop btcpay && sudo systemctl stop nbxplorer

```

```bash cd src/NBXplorer

```

## VERSION=2.5.

````bash git pull https://github.com/dgarage/NBXplorer.gitv$VERSION
``` From https://github.com/dgarage/NBXplorer- tag v2.4.3 -> FETCH_HEAD Updating c7b5a73..95f28ac Fast-forward Dockerfile.linuxamd | 4 +-
Dockerfile.linuxarm32v | 4 +-
Dockerfile.linuxarm64v | 4 +-
NBXplorer.Client/AssetMoney.cs | 1 -
[...] Se a mensagem lhe mostrar "fatal: unable to auto-detect email address (got 'btcpay@minibolt.(none)')" Se o prompt mostrar isso:

É necessário executar o comando anterior git pull novamente:
- Pressionar Ctrl+X quando o nano abre automaticamente o MERGE_MSG para não aplicar modificações
- Construir
```bash git config user.email "minibolt@dummyemail.com"
````

````bash git config user.name "MiniBolt"
``` hint: You have divergent branches and need to specify how to reconcile them.
hint: You can do so by running one of the following commands sometime before hint: your next pull:
hint:
hint: git config pull.rebase false # merge (the default
strategy) hint: git config pull.rebase true # rebase hint: git config pull.ff only # fast-forward only hint:
hint: You can replace "git config" with "git config --global" to set a default
hint: preference for all repositories. You can also pass --
rebase, --no-rebase,
hint: or --ff-only on the command line to override the configured default per hint: invocation.
```bash git config pull.rebase false
``` ./build.sh Exemplo de resultados esperados
- Verificar a atualização correta da instalação do resultado esperado:
- Inicie o servidor NBXplorer & BTCPay novamente. Monitorizar os registos com journalctl -fu nbxplorer & journalctl -fu btcpay para garantir que tudo está a correr bem
- Parar o servidor BTCPay MSBuild version 17.8.3+195e7f5a3 for .NET Determining projects to restore...
Restored /home/btcpay/src/NBXplorer/NBXplorer.Client/ NBXplorer.Client.csproj (in 2.43 sec).
Restored /home/btcpay/src/NBXplorer/NBXplorer/NBXplorer.csproj (in 2.47 sec).
NBXplorer.Client -> /home/btcpay/src/NBXplorer/NBXplorer.Client/ bin/Release/netstandard2.1/NBXplorer.Client.dll NBXplorer -> /home/btcpay/src/NBXplorer/NBXplorer/bin/Release/ net8.0/NBXplorer.dll Build succeeded.
0 Warning(s)
0 Error(s)
Time Elapsed 00:00:19.
head -n 6 /home/btcpay/src/NBXplorer/NBXplorer/NBXplorer.csproj | grep Version > <Version>2.4.3</Version>
```bash sudo systemctl start nbxplorer && sudo systemctl start btcpay
````

```bash sudo systemctl stop btcpay

```

- Entre na pasta `src/btcpayserver
- Definir a versão da variável de ambiente
- Obter as alterações da última tag. Pressionar Ctrl+X quando o nano abrir automaticamente o MERGE_MSG para aplicar as modificações do resultado esperado:
  Se o aviso lhe mostrar "fatal: unable to auto-detect email address (got 'btcpay@minibolt.(none)')"

```bash cd src/btcpayserver

```

## VERSION=1.13.

`bash git pull https://github.com/btcpayserver/btcpayserver.git` v$VERSION From https://github.com/btcpayserver/btcpayserver- tag v1.12.0 -> FETCH_HEAD Updating 541cef55b..6ecfe073e Fast-forward

## BTCPayServer.Data/ApplicationDbContext.cs | 2 +-

## BTCPayServer.Data/Data/AppData.cs | 10 +++++++++-

[...]

```bash git config user.email "minibolt@dummyemail.com"

```

````bash git config user.name "MiniBolt"
``` Se o prompt mostrar-lhe: fatal: Necessidade de especificar como reconciliar ramos divergentes.
- Construir Exemplo de resultados esperados
```bash git config pull.rebase false
``` ./build.sh Determining projects to restore...
Restored /home/btcpay/src/btcpayserver/
## BTCPayServer.Abstractions/BTCPayServer.Abstractions.csproj (in ms).
Restored /home/btcpay/src/btcpayserver/BTCPayServer.Client/
## BTCPayServer.Client.csproj (in 965 ms).
Restored /home/btcpay/src/btcpayserver/BTCPayServer.Common/
## BTCPayServer.Common.csproj (in 978 ms).
Restored /home/btcpay/src/btcpayserver/BTCPayServer.Data/
## BTCPayServer.Data.csproj (in 113 ms).
Restored /home/btcpay/src/btcpayserver/BTCPayServer.Rating/
## BTCPayServer.Rating.csproj (in 178 ms).
Restored /home/btcpay/src/btcpayserver/BTCPayServer/
## BTCPayServer.csproj (in 1.9 sec).
## BTCPayServer.Client -> /home/btcpay/src/btcpayserver/
## BTCPayServer.Client/bin/Release/netstandard2.1/
## BTCPayServer.Client.dll
## BTCPayServer.Common -> /home/btcpay/src/btcpayserver/
## BTCPayServer.Common/bin/Release/net8.0/BTCPayServer.Common.dll
## BTCPayServer.Rating -> /home/btcpay/src/btcpayserver/
## BTCPayServer.Rating/bin/Release/net8.0/BTCPayServer.Rating.dll
## BTCPayServer.Abstractions -> /home/btcpay/src/btcpayserver/
## BTCPayServer.Abstractions/bin/Release/net8.0/
## BTCPayServer.Abstractions.dll
## BTCPayServer.Data -> /home/btcpay/src/btcpayserver/
## BTCPayServer.Data/bin/Release/net8.0/BTCPayServer.Data.dll
## BTCPayServer -> /home/btcpay/src/btcpayserver/BTCPayServer/bin/ Release/net8.0/BTCPayServer.dll
## BTCPayServer -> /home/btcpay/src/btcpayserver/BTCPayServer/bin/ Release/publish/
- Verificar a atualização correta da instalação do resultado esperado:
- Inicie o servidor BTCpay novamente. Monitorize os registos com
journalctl -fu btcpay para garantir que tudo está a correr bem
- Parar o btcpay e o nbxplorer
- Desativar o arranque automático (se ativado)
- Eliminar os serviços btcpay e nbxplorer head -n 3 /home/btcpay/src/btcpayserver/Build/Version.csproj | grep Version > <Version>1.12.0</Version>
```bash sudo systemctl start btcpay
````

```bash sudo systemctl stop btcpay && sudo systemctl stop nbxplorer

```

```bash sudo systemctl disable btcpay && sudo systemctl disable nbxplorer

```

```bash sudo rm /etc/systemd/system/btcpay.service

```

```bash sudo rm /etc/systemd/system/nbxplorer.service

```

- Visualize as regras da firewall UFW e anote os números das regras para o servidor BTCPay (por exemplo, X e Y abaixo)
  Resultado esperado:
- Eliminar a regra com o número correto e confirmar com "sim".
- Editar o ficheiro torrc
- Comente ou remova o serviço oculto btcpay no torrc. Guardar e sair
- Recarregar a configuração torrc
- Eliminar as bases de dados nbxplorer e btcpay

````bash sudo ufw status numbered
``` > **[Y]** 23000 ALLOW IN Anywhere # allow BTCPay Server from anywhere
```bash sudo ufw delete X
````

```bash sudo nano +63 /etc/tor/torrc --linenumbers

```

# Hidden

Service BTCPay Server
#HiddenServiceDir /var/lib/tor/hidden_service_btcpay/
#HiddenServiceVersion
#HiddenServicePoWDefensesEnabled
#HiddenServicePort 80 127.0.0.1:

````bash sudo systemctl reload tor
``` Anterior
## Instalação Thunderhub (opcional)
Próximo
## Acesso Remoto via Tor (opcional)
Atualizado há 1 ano
```bash sudo -u postgres psql -c "DROP DATABASE nbxplorer;" && sudo -u
``` postgres psql -c "DROP DATABASE btcpay;" TCP Porto predefinido do PostgreSQL TCP Porto predefinido do NBXplorer TCP Porto predefinido do servidor BTCPay
````
