1.  # Preparação

Nesta etapa vamos separar todo o hardware necessário, preparar as suas
palavras‑passe e instalar o sistema operacional que servirá de base para o
seu nó.

Este guia parte do princípio de que você irá utilizar um computador pessoal
comum, facilmente encontrado no mercado. No entanto, ele também pode ser
adaptado para rodar em servidores na nuvem ou máquinas virtuais.

### Requisitos de hardware

Você precisará, no mínimo, de:

- Processador Intel/AMD (geração ≥ 2010).
- 4 GB de RAM para apenas Bitcoin, ou 8 GB de RAM (ou mais) se for
  utilizar também LND e aplicações adicionais.
- Armazenamento interno: SSD de 2 TB (ou superior).
- Pen drive de 32 GB (ou superior).
- Monitor temporário.
- Teclado temporário.

Opcionalmente, é recomendável ter também:

- UPS (Unidade de Alimentação Ininterrupta) para evitar desligamentos
  bruscos.

### Preparação das palavras‑passe

Ao longo do tutorial, você utilizará diversas palavras‑passe. É muito mais
simples anotá‑las todas no início do processo do que criá‑las às pressas
no meio da configuração.

Recomendações:

- Cada palavra‑passe deve ser única.
- Use pelo menos 12 caracteres.
- Misture letras maiúsculas, minúsculas, números e símbolos (como espaços,
  aspas simples ' ou aspas duplas ").

Sugestão de organização (anote em papel e guarde em local seguro):

- **[A]** Palavra‑passe do utilizador administrador principal.
- **[B]** Palavra‑passe Bitcoin RPC.
- **[C]** Palavra‑passe da carteira LND.
- **[D]** Palavra‑passe do BTC‑RPC‑Explorer (opcional).
- **[E]** Palavra‑passe do ThunderHub.

### Segurança da rede doméstica

Embora este guia mostre como proteger o seu nó, você continuará a interagir
com ele a partir do seu computador e do seu telemóvel, utilizando a sua rede
doméstica.

Antes de construir o seu MiniBolt, é fortemente recomendado que você
reforce a segurança da sua rede doméstica e dos seus dispositivos.

Um bom ponto de partida (em inglês) é o tutorial "How to Secure Your Home
Network Against Threats", de Heinrich Long. Procure aplicar o maior número
possível de recomendações, lembrando que alguns pontos podem não se
aplicar ao seu roteador/dispositivo.

### Instalação do Ubuntu Server

Utilizaremos o sistema operacional **Ubuntu Server LTS (Long Term Support)**,
sem interface gráfica. Essa escolha oferece maior estabilidade e torna a
configuração inicial muito mais simples.

O Ubuntu Server é baseado na distribuição Linux Debian e está disponível
para a maioria das plataformas de hardware. Para tornar este guia o mais
universal possível, utilizamos apenas comandos padrão baseados em Debian.
Como resultado, ele funciona bem tanto em computadores pessoais quanto na
maioria das demais plataformas compatíveis.

Use as teclas do teclado para navegar pelos menus de instalação e siga as
instruções abaixo.

1. No primeiro ecrã, selecione o idioma de sua preferência.
2. Se for oferecida uma atualização do instalador, selecione a opção para
   atualizar, pressione Enter e aguarde.
3. Selecione o layout e a variante do teclado e pressione Enter.
4. Na tela de tipo de instalação, mantenha a opção padrão do Ubuntu
   Server e prossiga.
5. Selecione a interface de rede que deseja utilizar (recomenda‑se
   **Ethernet**) e anote o endereço IP obtido automaticamente por DHCP
   (geralmente algo como `192.168.x.xx`). Em seguida, prossiga.

Por padrão, o roteador reserva esse endereço IP por algum tempo. Porém,
se o equipamento ficar desligado durante um período maior, ele poderá
receber um IP diferente na próxima inicialização, o que dificultaria o acesso
ao nó.

Para evitar isso, no assistente de instalação do Ubuntu você pode definir
um IP fixo (estático) para a máquina, escolhendo um endereço livre dentro
da sua rede local.

- Deixe a opção de **proxy HTTP** em branco, a menos que você saiba que
  precisa de um.
- Caso não queira utilizar um mirror alternativo para o Ubuntu, deixe essa
  opção em branco e prossiga.

Na etapa de particionamento do disco, há duas opções principais:

- Utilizar um único disco para sistema e dados.
- Utilizar um disco para o sistema e outro disco separado para dados
  (blockchain, índices, etc.).

Se quiser usar um segundo disco apenas para os dados da blockchain,
consulte o capítulo específico de "Uso de segundo disco" para instruções
detalhadas antes de prosseguir.

Confirme as alterações de particionamento (atenção: isso apaga os dados
existentes no disco selecionado) e continue com a instalação.

Na tela de criação do usuário, vamos usar um usuário temporário, pois o
nome **admin** será reservado para o usuário final que criaremos depois.

Preencha da seguinte forma:

- **Nome:** temp
- **Usuário:** temp
- **Nome do servidor (hostname):** minibolt
- **Palavra‑passe:** use a senha **[A]**

Marque a opção para permitir SSH (se disponível durante a instalação) e
prossiga sem selecionar softwares adicionais, a menos que você tenha um
motivo específico.

O instalador aplicará todas as configurações e copiará os arquivos do
sistema. Esse processo pode levar alguns minutos, dependendo do
hardware.

Ao final, selecione a opção para reiniciar o sistema, remova o pen drive
quando solicitado e deixe o computador iniciar normalmente até o prompt de
login.

Depois disso, você já poderá desconectar o monitor e o teclado do MiniBolt e
passar a trabalhar apenas por acesso remoto (SSH) a partir do seu
computador principal.

## DHCP

Agora é hora de se conectar ao BRLNBolt via Secure Shell SSH) e começar
a trabalhar em outra maquina da mesma rede. Para isso, precisamos de um cliente SSH.
Instale e inicie o cliente SSH para o seu sistema operativo:
, 2 opções:
◦Transfira a versão 64-bit x ou 32-bit x , dependendo da arquitetura do seu SO. Fonte
▪Inicie o Putty, na árvore da esquerda, selecione "session", na caixa "Hostname (or IP address)", escreva temp@192.168.x.xx , porta 22 na caixa da esquerda.
▪Premir o botão "OPEN", quando aparecer a mensagem "Alerta de
segurança PuTTy", prima a tecla "Accept", e, finalmente, digite a sua password **[A]** .

- Descarregar a versão Portable Edition ou Installer Edition, consoante pretenda instalá-la permanentemente ou não.
  ◦Iniciar o MobaXterm, 2 opções:
  ▪Se quiser guardar a sessão para mais tarde: no menu superior, clique em "Sessão"  "Nova sessão"  Selecione "SSH".
- Introduza o endereço IP do MiniBolt 192.168.x.xx), selecione "specify username" e introduza à direita "temp", mantenha a porta "22" selecionada à direita.
- Premir o botão OK, quando aparecer a mensagem "Connexion
  to...", premir o botão "Accept" e, por fim, digitar a sua "password A`.
- Caso contrário, selecione no painel de controlo o botão "Iniciar terminal local" e escreva diretamente no terminal ssh temp@192.168.x.xxx .
  ◦No terminal nativo, digite: ssh temp@192.168.x.xxx
  ◦Use o Putty, simplesmente no terminal nativo digite sudo apt
  install putty e inicie-o digitando putty , siga as mesmas instruções do Putty para Windows.
  Nota, pormenores de ligação:
  Vamos trabalhar com a linha de comandos do PC, que pode ser uma
  novidade para si. Encontre algumas informações básicas abaixo. Elas ajudá-lo-ão a navegar e a interagir com o seu PC.
  O utilizador introduz comandos e o PC responde imprimindo os resultados
  por baixo do seu comando. A resposta do sistema é assinalada com o carácter > .
  Os comentários adicionais começam por # e não fornecem qualquer ação, apenas servem para se orientar.
  No exemplo a seguir, basta digitar ls -la e pressionar a tecla enter/return:
  > hostname: o seu endereço IP Ubuntu (MiniBolt) como:
  > 192.168.x.xxx > port:
  > username: temp > password: password **[A]** ls -la > exemplo de resposta do sistema

# Isto

é um comentário
: pode utilizar a tecla Tab para auto-completar quando introduz comandos, isto é, para comandos, diretórios ou nomes de ficheiros.
: premindo (seta para cima) e (seta para baixo) no seu teclado, pode chamar os comandos introduzidos anteriormente.
: nosso usuário comum não tem
privilégios diretos de administrador. Se um comando precisa editar a

## configuração do sistema, devemos utilizar o comando sudo ("superuser

do") como prefixo. Ao invés de editar um arquivo de sistema com nano /etc/fstab , nós usamos sudo nano /etc/fstab .
Por razões de segurança, os utilizadores de serviços como "bitcoin" não podem utilizar o comando sudo .
: utilizamos o editor Nano para criar novos
ficheiros de texto ou editar os existentes. Não é complicado, mas guardar e sair não é intuitivo.
◦Guardar: premir Ctrl-O (para Saída), confirmar o nome do ficheiro e premir a tecla Enter .
◦Sair: premir Ctrl-X
: se estiver a utilizar o Windows e o cliente SSH PuTTY,
pode copiar texto da shell selecionando-o com o rato (não é necessário
clicar em nada), e colar coisas na posição do cursor com um clique no
botão direito do rato em qualquer parte da janela ssh.
Em outros programas do Terminal, copiar/colar geralmente funciona com
Ctrl - Shift - C e Ctrl - Shift - V .
Utilizaremos o usuário principal admin em vez de temp para tornar este guia mais universal.

- Criar um novo utilizador chamado admin com a sua password **[A]**
- Torne este novo usuário um superusuário, adicionando-o aos grupos de usuários sudo e temp antigo
- Terminar a sessão do utilizador temp existente
- Repita Access with Secure Shell mas, desta vez, faça o login com admin e seu password **[A]**
- Apage o utilizador temp . Não se preocupe com a mensagem userdel:
  temp mail spool (/var/mail/temp) not found Saída Esperada:
  Para alterar a configuração do sistema e os ficheiros que não pertencem ao
  utilizador "admin", é necessário prefixar os comandos com sudo . De
  tempos em tempos, será solicitado que você digite sua password **[A]** de administrador para aumentar a segurança
- Atualizar o sistema operativo e todos os pacotes de software instalados

```bash sudo adduser --gecos "" admin

```

````bash sudo usermod -a -G sudo,adm,cdrom,dip,plugdev,lxd admin
``` logout
```bash sudo userdel -rf temp
``` > userdel: temp mail spool (/var/mail/temp) not found
```bash sudo apt update && sudo apt full-upgrade
````

- Para podermos utilizar o nome de anfitrião minibolt em vez do
  endereço IP, temos de instalar este pacote de software necessário
  Uma unidade de armazenamento de alto desempenho é essencial para o seu Node.
  Vamos verificar se o seu drive está funcionando na velocidade adequada
  Seu disco deve ser dectado como /dev/sda. Verifique se este é o caso listando os nomes dos dispositivos com o comando abaixo:
  Meça a velocidade do seu drive

```bash sudo apt install avahi-daemon

```

# Verifique

o desempenho do drive

# Unidade

de armazenamento de alto desempenho é essencial para o seu node.

# Vamos

verificar se o seu drive está funcionando bem como está.

# Seu

disco deve ser detectado como /dev/sda. Verifique se este é
o caso listando os nomes dos dispositivos de bloco conectados lsblk -pli

````bash sudo hdparm -t --direct /dev/sda
``` Timing O_DIRECT disk reads: 932 MB in 3.00 seconds = 310.23 MB/sec
Vamos armazenar todos os dados da aplicação no diretório dedicado /
data . Isto permite uma maior segurança porque não se encontra no diretório
pessoal de nenhum utilizador. Além disso, é mais fácil mover esse diretório
para outro local, por exemplo, para uma unidade separada, uma vez que pode simplesmente montar qualquer opção de armazenamento em /data
- Criar a pasta de dados Atribuição ao usuário admin como proprietário da pasta /data
Vamos assegurar que o seu MiniBolt esteja protegido contra o acesso remoto não autorizado.
```bash sudo hdparm -t --direct /dev/sdb
``` Timing O_DIRECT disk reads: 932 MB in 3.00 seconds = 310.23 MB/sec
```bash sudo mkdir /data
````

````bash sudo chown admin:admin /data
``` O BRLNBolt tem de ser protegido contra ataques em linha utilizando vários métodos.
Uma firewall controla o tipo de tráfego externo que a sua máquina aceita e
quais as aplicações que podem enviar dados. Por defeito, muitas portas de
rede estão abertas e à espera de ligações de entrada. Fechar portas desnecessárias pode reduzir muitas vulnerabilidades potenciais do sistema.
Por enquanto, apenas SSH deve ser acessível do lado de fora. Bitcoin Core e
LND estão usando Tor e não precisam de portas de entrada. Nós abriremos a porta para outras aplicações web mais tarde, se necessário.
- Com o usuário admin , verifique a sua disponibilidade de IPv
Se obtiver ping6: connect: Network is unreachable , não tem
disponibilidade de IPv6, mas não se preocupe, a adoção do IPv6 é recente,
utilizará a sua ligação à Internet utilizando o IPv4 comum. Além disso, pode obter o seu IPv4 público com: curl -s ipv4.icanhazip.com
Se obtiver a saída "OK." , tem disponibilidade de IPv6, adicionalmente, pode
obter o seu IPv6 com: curl -s ipv6.icanhazip.com você está , continue o guia sem modificações
Se não tiver disponibilidade de IPv6, pode desativar o IPv6 no UFW para evitar a criação de regras relacionadas com o mesmo:
- Editar a configuração do UFW
- Alterar IPV6=yes para IPV6=no . Guardar e sair
- Desativar o registo ping6 -c2 2001:858:2:2:aabb:0:563b:1526 && ping6 -c 2620:13:4000:6000::1000:118 && ping6 -c2 2001:67c:289c::9 && ping
-c2 2001:678:558:1000::244 && ping6 -c 2001:638:a000:4140::ffff:189 && echo OK.
```bash sudo nano /etc/default/ufw
``` IPV6=no
```bash sudo ufw logging off
````

- Permitir a ligação de entrada SSH
- Ativar o UFW, quando o aviso lhe mostrar "Command may disrupt existing ssh connections. Proceed with operation (y|n)?" , prima "y" e enter Resultado esperado:
- Verificar se o UFW está corretamente configurado e ativo Resultado esperado Atenção! Não esqueça do passo seguinte!

```bash sudo ufw allow 22/tcp comment 'allow SSH from anywhere'

```

````bash sudo ufw enable
``` > Firewall is active and enabled on system startup
```bash sudo ufw status verbose
``` > Status: active > Logging: off > Default: deny (incoming), allow (outgoing), disabled (routed)
> New profiles: skip > To Action From > -- ------ ----
> 22 ALLOW Anywhere # allow SSH from anywhere
Se, por engano, a porta estiver bloqueada, pode ligar um teclado e um ecrã
ao seu PC para iniciar sessão localmente e corrigir estas definições (especialmente para a porta SSH 22 Mais informações: UFW Essentials

Configuramos o Tor para que o seu nó funcione de forma anónima.
direto e soberano na rede Bitcoin. No entanto, se não for configurado sem
privacidade em mente, ele também diz ao mundo que há alguém com Bitcoin nesse endereço.
Também facilitaremos a ligação ao seu nó a partir de fora da sua rede doméstica como uma vantagem adicional.
É verdade que apenas o seu endereço IP é revelado, mas utilizando serviços como iplocation.net , o seu endereço físico pode ser determinado com
bastante exatidão. Especialmente com o Lightning, o seu endereço IP seria
amplamente utilizado. Temos de nos certificar de que mantém a sua privacidade.

Utilizamos o Tor, um software gratuito criado pelo Tor Project . Permite-lhe
tornar anónimo o tráfego da Internet, encaminhando-o através de uma rede
de nós, ocultando a sua localização e perfil de utilização.
Chama-se "Tor" como acrónimo de "The Onion Router": a informação é
encaminhada através de muitos saltos e encriptada várias vezes. Cada nó
decifra apenas a camada de informação que lhe é dirigida, sabendo apenas
o salto anterior e o seguinte de todo o percurso. O pacote de dados é descascado como uma cebola até chegar ao destino final.
- Com o usuário admin , atualize os pacotes para se manter atualizado com o SO
```bash sudo apt update && sudo apt full-upgrade
````

- Instalar a dependência
- Criar um novo ficheiro chamado tor.list
- Acrescentar as seguintes entradas. Guardar e sair
- Vá temporatiamente para o usuário "root"
- Adicione a chave GPG utilizada para assinar os pacotes executando o seguinte comando na sua linha de comandos
- Regresse ao admin usando o comando exit

```bash sudo apt install apt-transport-https

```

````bash sudo nano /etc/apt/sources.list.d/tor.list
``` deb [arch=amd64 signed-by=/usr/share/keyrings/tor-archive-keyring.gpg] https://deb.torproject.org/torproject.orgjammy main deb-src [arch=amd64 signed-by=/usr/share/keyrings/tor-archive-keyring.gpg] https://deb.torproject.org/torproject.orgjammy main
```bash sudo su
````

`bash wget -qO- https://deb.torproject.org/torproject.org/` A3C4F0F979CAA22CDBA8F512EE8CBC9E886DDD89.asc | gpg --dearmor | tee /usr/share/keyrings/tor-archive-keyring.gpg >/dev/null

- Actualize o repositório apt, e instale o Tor e o Tor Debian keyring. Prima "y" e "enter"
- Verificar se o Tor foi corretamente instalado do resultado esperado:
  Tenha em atenção que o número da versão anterior pode mudar no seu
  caso, este é apenas um exemplo de quando o guia foi criado.
  O Bitcoin Core irá se comunicar diretamente com o daemon Tor para rotear
  todo o tráfego através da rede Tor. Nós precisamos habilitar o Tor para
  aceitar instruções através de sua porta de controle, com a autenticação apropriada.
- Editar a configuração do Tor exit

````bash sudo apt update && sudo apt install tor deb.torproject.org-keyring
``` tor --version > Tor version 0.4.7.13.
[...]
- Descomente a para ativar o porto de controlo, eliminando o # no início da linha. Guardar e sair Descomente
- Recarregar a configuração do Tor para ativar as modificações
- Certifique-se de que o serviço Tor está funcionando e escutando nos portos padrão 9050 e 9051 no localhost 127.0.0.1 Resultado esperado
Verifique o diário do systemd para ver Tor em tempo real
atualizando os logs de saída. Ctrl + C para sair do resultado esperado
```bash sudo nano +56 /etc/tor/torrc --linenumbers
``` ControlPort
```bash sudo systemctl reload tor
````

````bash sudo ss -tulpn | grep LISTEN | grep tor
``` tcp LISTEN 0 4096 127.0.0.1:9050 0.0.0.0:* users:
(("tor",pid=795,fd=6)) tcp LISTEN 0 4096 127.0.0.1:9051 0.0.0.0:* users:
(("tor",pid=795,fd=7)) journalctl -fu tor@default
Dec 11 10:47:04 minibolt Tor[1065]: Tor 0.4.7.11 running on Linux with Libevent 2.1.12-stable, OpenSSL 3.0.2, Zlib 1.2.11, Liblzma 5.2.5, Libzstd 1.4.8 and Glibc 2.35 as libc.
Dec 11 10:47:04 minibolt Tor[1065]: Tor can't help you if you use it wrong! Learn how to be safe at https://support.torproject.org/faq/staying-anonymous/ Dec 11 10:47:04 minibolt Tor[1065]: Read configuration file "/usr/ share/tor/tor-service-defaults-torrc".
Dec 11 10:47:04 minibolt Tor[1065]: Read configuration file "/etc/ tor/torrc".
Dec 11 10:47:04 minibolt Tor[1065]: Based on detected system
memory, MaxMemInQueues is set to 2751 MB. You can override this by setting MaxMemInQueues by hand.
Dec 11 10:47:04 minibolt Tor[1065]: Opening Socks listener on 127.0.0.1:
Dec 11 10:47:04 minibolt Tor[1065]: Opened Socks listener connection (ready) on 127.0.0.1:
Dec 11 10:47:04 minibolt Tor[1065]: Opening Control listener on 127.0.0.1:
Dec 11 10:47:04 minibolt Tor[1065]: Opened Control listener connection (ready) on 127.0.0.1:
[...] Dec 11 10:47:36 minibolt Tor[1065]: Bootstrapped 75% (enough_dirinfo): Loaded enough directory info to build circuits Dec 11 10:47:37 minibolt Tor[1065]: Bootstrapped 89% (ap_handshake): Finishing handshake with a relay to build circuits Dec 11 10:47:37 minibolt Tor[1065]: Bootstrapped 90% (ap_handshake_done): Handshake finished with a relay to build circuits Dec 11 10:47:37 minibolt Tor[1065]: Bootstrapped 95% (circuit_create): Establishing a Tor circuit Dec 11 10:47:37 minibolt Tor[1065]: Bootstrapped 100% (done): Done Nov 13 23:19:20 minibolt systemd[1]: Reloading tor@default.service
- Anonymizing overlay network for TCP...
Nov 13 23:19:20 minibolt Tor[27155]: Received reload signal (hup).
Reloading config and resetting internal state.
Nov 13 23:19:20 minibolt Tor[27155]: Read configuration file "/ usr/share/tor/tor-service-defaults-torrc".
Nov 13 23:19:20 minibolt Tor[27155]: Read configuration file "/ etc/tor/torrc".
Nov 13 23:19:20 minibolt Tor[27155]: Opening Control listener on 127.0.0.1:
Nov 13 23:19:20 minibolt Tor[27155]: Opened Control listener connection (ready) on 127.0.0.1:
Nov 13 23:19:20 minibolt systemd[1]: Reloaded tor@default.service
- Anonymizing I2P
é uma camada de rede anônima universal. Todas as comunicações
através do I2P são anônimas e criptografadas de ponta a ponta, e os
participantes não revelam seus endereços IP reais. O I2P permite que
pessoas de todo o mundo se comuniquem e compartilhem informações sem restrições.
O cliente I2P é um software usado para construir e utilizar redes anônimas
I2P. Essas redes são comumente usadas para aplicativos anônimos de peer-to-peer (compartilhamento de arquivos, criptomoedas) e aplicativos anônimos cliente-servidor (sites, mensageiros instantâneos, servidores de chat).
Vamos usar o i2pd I2P Daemon), uma implementação completa do cliente I2P em C, como um complemento à rede Tor.
Saída esperada:
Atualize o repositório apt e instale o i2pd como qualquer outro pacote de
software. Pressione "y" e enter ou diretamente enter quando solicitado
```bash wget -q -O - https://repo.i2pd.xyz/.help/add_repo| sudo bash -s -
``` Importando chave de assinatura Adicionando repositório APT
```bash sudo apt update && sudo apt install i2pd
``` Verifique se o i2pd foi instalado corretamente Exemplo de saída esperada:
Certifique-se de que o serviço i2pd está funcionando e ouvindo nas portas
padrão Veja o “i2p” em ação monitorando seu arquivo de log. Saia com Ctrl-C i2pd --version i2pd version 2.44.0 (0.9.56)
[...]
```bash sudo ss -tulpn | grep i2pd
``` udp UNCONN 0 0 127.0.0.1:7655 0.0.0.0:* users:(("i2pd",pid=1305094,fd=45)) udp UNCONN 0 0 0.0.0.0:20003 0.0.0.0:* users:(("i2pd",pid=1305094,fd=21)) tcp LISTEN 0 4096 0.0.0.0:20003 0.0.0.0:* users:(("i2pd",pid=1305094,fd=20)) tcp LISTEN 0 4096 127.0.0.1:7656 0.0.0.0:* users:(("i2pd",pid=1305094,fd=44)) tcp LISTEN 0 4096 127.0.0.1:6668 0.0.0.0:* users:(("i2pd",pid=1305094,fd=40)) tcp LISTEN 0 4096 127.0.0.1:7070 0.0.0.0:* users:(("i2pd",pid=1305094,fd=25)) tcp LISTEN 0 4096 127.0.0.1:4444 0.0.0.0:* users:(("i2pd",pid=1305094,fd=35)) tcp LISTEN 0 4096 127.0.0.1:4447 0.0.0.0:* users:(("i2pd",pid=1305094,fd=36))
```bash sudo tail -f /var/log/i2pd/i2pd.log
``` Opcional)  Se desejar, você pode desativar a opção de inicialização automática para o I2P usando:
Saída esperada:
Anterior
## LN BOLT Próximo
## Instalação Bitcoin Core Atualizado há 1 ano 11:52:56@883/none - i2pd v2.44.0 (0.9.56) iniciando...
11:52:57@444/warn - Transports: 15 chaves efêmeras geradas no momento 11:52:57@883/warn - Addressbook: o uso de subscriptions.txt está obsoleto, use o arquivo de configuração em vez disso 11:52:58@783/warn - SSU2: Peer test 4 roteador não encontrado 11:52:58@783/warn - SSU2: Peer test 4 roteador não encontrado 11:53:02@783/warn - SSU2: Sessão com 81.155.117.241:24027 não foi estabelecida após 5 segundos 11:53:02@783/warn - SSU2: Sessão com 82.48.155.160:20423 não foi estabelecida após 5 segundos 11:53:02@783/warn - SSU2: Sessão com 81.107.248.153:24716 não foi estabelecida após 5 segundos 11:53:02@783/warn - SSU2: Sessão com 188.127.17.98:39249 não foi estabelecida após 5 segundos 11:53:02@553/warn - NTCP2: Erro ao ler SessionCreated: Fim do arquivo
```bash sudo systemctl disable i2pd
``` > Sincronizando o estado do i2pd.service com o script do serviço SysV com /lib/systemd/systemd-sysv-install.
> Executando: /lib/systemd/systemd-sysv-install disable i2pd > Removido /etc/systemd/system/multi-user.target.wants/ i2pd.service.
````
