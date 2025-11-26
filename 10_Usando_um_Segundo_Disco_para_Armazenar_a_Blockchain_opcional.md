# Usando
 um Segundo Disco para Armazenar a Blockchain (opcional)
Poderá ter o interesse em usar um segundo disco no seu setup. Vejamos os seguintes cenários
- O disco está a ficar cheio.
- Precisa de minimizar os riscos e aumentar a redundancia.
- Sente necessidade de partilhar a blockchain com mais pessoas.
Para reduzir o potencial de corrupção de dados, não queremos que nenhum dos serviços esteja a funcionar enquanto trabalhamos nesta atualização.
Pare e desative cada serviço Escolha um ou vários conforme a sua realidade.
## Usando um Segundo Disco para Armazenar a Blockchain (opcional) ...
É importante manter o sistema atualizado com patches de segurança e actualizações de aplicações.
Faça isso regularmente a cada poucos meses para obter atualizações relacionadas à segurança.
Certifique-se de que todos os pacotes de software necessários estão instalados:
Para armazenar a blockchain, precisamos de muito espaço. Como uma
## instalação de servidor, o sistema de ficheiros nativo do Linux Ext4 é a melhor
escolha para o disco rígido externo, por isso vamos formatar o disco rígido,
apagando todos os dados anteriores. O disco rígido externo é então anexado
ao sistema de ficheiros e pode ser acedido como uma pasta normal (a isto chama-se "montagem").
```bash $ sudo systemctl stop bitcoind
```
```bash $ sudo systemctl disable bitcoind.service
```
```bash $ sudo systemctl stop lnd
```
```bash $ sudo systemctl disable lnd.service
```
```bash $ sudo systemctl stop btcrpcexplorer
```
```bash $ sudo systemctl disable btcrpcexplorer.service
```
```bash $ sudo systemctl stop electrs
```
```bash $ sudo systemctl disable electrs.service
```
```bash sudo apt update && sudo apt full-upgrade
```
```bash sudo apt install htop git curl bash-completion jq qrencode --
``` install-recommends
## Usando um Segundo Disco para Armazenar a Blockchain (opcional) ...
- Liste todos os dispositivos com informações adicionais. A lista mostra os
dispositivos (por exemplo, sdb ) e, se existirem, as partições que contêm (por exemplo, sdb1 ).
Tome nota do nome da partição que pretende utilizar (neste caso, "sdb1").
- No exemplo acima, a unidade externa original é sda e tem a partição
sda1 . A unidade externa recém-anexada é sdb e ainda não tem
nenhuma partição. É muito importante manter o controle de qual
dispositivo de bloco e partição se aplica à unidade original e à nova unidade.
lsblk -o NAME,MOUNTPOINT,UUID,FSTYPE,SIZE,LABEL,MODEL
## RESPOSTA ESPERADA...
## > NAME MOUNTPOINT UUID
## FSTYPE SIZE LABEL MODEL > sda 931.5G BUP_Slim_RD > └─sda1 /mnt/ext 3aab0952-3ed4-4652-b203-d994c4fdff20 ext
## 931.5G > sdb
## 953.9G SABRENT > mmcblk 58G > ├─mmcblk0p1 /boot 4BBD-D3E7 vfat 256M boot > └─mmcblk0p2 / 45e99191-771b-4e12-a526-0779148892cb ext 57.8G rootfs
## Usando um Segundo Disco para Armazenar a Blockchain (opcional) ...
- Formate a partição no disco externo com Ext4 (use o [NOME] de cima, por exemplo, sdb1 )
- Liste os dispositivos mais uma vez e copie o UUID da nova partição para um editor de texto na sua máquina principal.
Resultado esperado
- Edite o arquivo fstab e adicione o seguinte como uma nova linha no final, substituindo 123456 pelo seu próprio UUID .
Aqui está um exemplo do novo ponto de montagem para a nova unidade ao lado da unidade original
```bash sudo mkfs.ext4 /dev/[NAME]
``` lsblk -o NAME,MOUNTPOINT,UUID,FSTYPE,SIZE,LABEL,MODEL
## > NAME MOUNTPOINT UUID
## FSTYPE SIZE LABEL MODEL > sda 931.5G BUP_Slim_RD > └─sda1 /mnt/ext 3aab0952-3ed4-4652-b203-d994c4fdff ext4 931.5G > sdb
## 953.9G SABRENT > └─sdb1 1d9e9dee-87c3-4296-94e2-e833b948a19d ext4 953.9G > mmcblk 58G > ├─mmcblk0p1 /boot 4BBD-D3E vfat 256M boot > └─mmcblk0p2 / 45e99191-771b-4e12-a526-0779148892cb ext4 57.8G rootfs
```bash sudo nano /etc/fstab
``` UUID=123456 /mnt/blockchain ext rw,nosuid,dev,noexec,noatime,nodiratime,auto,nouser,async,nofa il 0 proc /proc proc defaults PARTUUID=738a4d67-01 /boot vfat defaults PARTUUID=738a4d67-ext defaults noatime
## Usando um Segundo Disco para Armazenar a Blockchain (opcional) ...
mais: Como funciona o fstab - introdução ao ficheiro /etc/fstab no Linux
- Criar o diretório para adicionar o disco rígido e definir o proprietário correto
- Reinicie o daemon.
Monte todas as unidades e verifique o sistema de ficheiros. O ficheiro "/ mnt/blockchain" está listado?
Resultado esperado.
PARTUUID=738a4d67-02 / ext4 defaults,noatime UUID=3aab0952-3ed4-4652-b203-d994c4fdff20 /mnt/ext ext rw,nosuid,dev,noexec,noatime,nodiratime,auto,nouser,async,nofa il 0 UUID=1d9e9dee-87c3-4296-94e2-e833b948a19d /mnt/blockchain ext rw,nosuid,dev,noexec,noatime,nodiratime,auto,nouser,async,nofa il 0
# a
 swapfile is not a swap partition, no line here
# use
 dphys-swapfile swap[on|off] for that
```bash sudo mkdir -p /mnt/blockchain
```
```bash systemctl daemon-reload
```
```bash sudo mount -a
``` df -h /mnt/blockchain > Filesystem Size Used Avail Use% Mounted on > /dev/sdb1 938G 77M 891G 1% /mnt/blockchain
Vamos utilizar o rsync para copiar os ficheiros, preservando as permissões e os atributos alargados
```bash cd /
```
```bash sudo rsync -avxHAX --numeric-ids --info=progress2 /data/bitcoin
``` /mnt/blockchain
## Usando um Segundo Disco para Armazenar a Blockchain (opcional) ...
O resultado mostrará a progressão do ficheiro

Embora a leitura de um disco e a escrita noutro possa ter um bom
desempenho, não se surpreenda se isto demorar algumas horas. Se não
estiver familiarizado com o rsync, veja como interpretar a saída acima por coluna
## 1. nome do ficheiro e caminho relativo
## 2. percentagem global de conclusão
## 3. velocidade de transferência
## 4. tempo restante (e.g. 10417) e depois mudou para tempo decorrido 00025
## 5. xfr é o número do ficheiro transferido
## 6. ir-chk=4324/4334 é a verificação de recursão incremental. ficheiros restantes / ficheiros totais
Ao longo da sincronização, a verificação de recursão incremental pode
aumentar até que transite para mostrar to-chk em vez de ir-chk , como
ilustrado abaixo. Quando isso acontece, ele descobriu todos os arquivos a serem copiados.
> sending incremental file list > ./ > bitcoin/ > bitcoin/.lock > 2,147,483,648 0% 81.22MB/s 0:00:25 (xfr#2, ir-chk=4327/4334)
> bitcoin/.walletlock > 2,147,483,648 0% 81.22MB/s 0:00:25 (xfr#3, ir-chk=4326/4334)
> bitcoin/banlist.dat > 2,147,483,685 0% 80.19MB/s 0:00:25 (xfr#4, ir-chk=4325/4334)
> bitcoin/bitcoin.conf > 2,147,484,131 0% 80.16MB/s 0:00:25 (xfr#5, ir-chk=4324/4334)
> bitcoin/db.log > 2,147,484,131 0% 80.16MB/s 1:04:
> ...
## Usando um Segundo Disco para Armazenar a Blockchain (opcional) ...
E quando terminar, deverá ter o seguinte aspeto Confirme que o novo local tem o conteudo esperado.
Apague o link simbolico anterior > bitcoin/indexes/txindex/206971.ldb > 360,288,743,724 84% 59.23MB/s 1:36:41 (xfr#19033, to-chk=1695/20739)
> bitcoin/indexes/txindex/206972.ldb > 360,290,914,611 84% 59.23MB/s 1:36:41 (xfr#19034, to-chk=1694/20739)
> bitcoin/indexes/txindex/206973.ldb > 360,293,085,490 84% 59.23MB/s 1:36:41 (xfr#19035, to-chk=1693/20739)
> bitcoin/indexes/txindex/206974.ldb > 360,295,256,251 84% 59.23MB/s 1:36:41 (xfr#19036, to-chk=1692/20739)
> bitcoin/indexes/txindex/206975.ldb > 360,297,427,362 84% 59.22MB/s 1:36:41 (xfr#19037, to-chk=1691/20739)
> bitcoin/indexes/txindex/206978.ldb > 360,299,598,549 84% 59.22MB/s 1:36:41 (xfr#19038, to-chk=1690/20739)
> bitcoin/indexes/txindex/206979.ldb > 360,301,769,513 84% 59.22MB/s 1:36:42 (xfr#19039, to-chk=1689/20739)
> bitcoin/indexes/txindex/206980.ldb > lost+found/ > 426,795,633,281 100% 54.07MB/s 2:05:28 (xfr#20717, to-chk=0/20739)
> sent 426,901,227,575 bytes received 393,910 bytes 56,674,626.15 bytes/sec > total size is 426,795,633,281 speedup is 1.
ls -la /mnt/blockchain/bitcoin
```bash sudo rm /home/bitcoin/.bitcoin
```
## Usando um Segundo Disco para Armazenar a Blockchain (opcional) ...
Confirme que o link já não existe.
- Mudar para o utilizador bitcoin
- Crie a ligação simbólica .bitcoin que aponta para esse diretório
- Verificar se a ligação simbólica foi criada corretamente Resultado esperado:
Sair da sessão do utilizador bitcoin e voltar ao utilizador admin
Definir permissões: apenas o utilizador bitcoin e membros do grupo
```bash bitcoin podem ler (necessário para o LND ler a linha " rpcauth ")
``` ls -la /home/bitcoin
```bash sudo su - bitcoin
``` ln -s /mnt/blockchain/bitcoin /home/bitcoin/.bitcoin ls -la
total drwxr-xr-x 3 bitcoin bitcoin 4096 Nov 7 19:33 .
drwxr-xr-x 4 root root 4096 Nov 7 19:32 ..
-rw------- 1 bitcoin bitcoin 135 Nov 7 19:33 .bash_history
-rw-r--r-- 1 bitcoin bitcoin 220 Nov 7 19:32 .bash_logout
-rw-r--r-- 1 bitcoin bitcoin 3523 Nov 7 19:32 .bashrc
lrwxrwxrwx 1 bitcoin bitcoin 13 Nov 7 19:32 .bitcoin -> /mnt/
blockchain/bitcoin drwxr-xr-x 3 bitcoin bitcoin 4096 Nov 7 19:33 .local
-rw-r--r-- 1 bitcoin bitcoin 1670 Nov 7 19:32 .mkshrc
-rw-r--r-- 1 bitcoin bitcoin 807 Nov 7 19:32 .profile exit
## Usando um Segundo Disco para Armazenar a Blockchain (opcional) ...
Vincule o diretório de dados do Bitcoin também a partir do diretório home do
usuário admin . Isso permite que o usuário admin trabalhe com o bitcoind diretamente, por exemplo, usando o comando bitcoin-cli Esta ligação simbólica fica ativa Faça logout do SSH digitando o seguinte comando
- Inicie novamente a sessão como utilizador admin abrindo uma nova sessão SSH
- Verificar se a ligação simbólica foi criada corretamente Resultado esperado:
## SOMENTE SE NÃO OBTEVE O RESULTADO
ESPERADO ( .bitcoin -> /mnt/blockchain/bitcoin ) e se só tiver
( .bitcoin ) ou ( .bitcoin-> /data/bitcoin ), deve seguir os passos seguintes para resolver o problema:
```bash sudo chmod 640 /home/bitcoin/.bitcoin/bitcoin.conf
``` ln -s /mnt/blockchain/bitcoin /home/admin/.bitcoin exit ls -la drwxr-xr-x 11 root root 4096 Oct 26 19:19 ..
-rw-rw-r-- 1 admin admin 12020 Nov 7 09:51 .bash_aliases
-rw------- 1 admin admin 51959 Nov 7 12:19 .bash_history
-rw-r--r-- 1 admin admin 220 Nov 7 20:25 .bash_logout
-rw-r--r-- 1 admin admin 3792 Nov 7 07:56 .bashrc
lrwxrwxrwx 1 admin admin 13 Nov 7 10:41 .bitcoin -> /mnt/ blockchain/bitcoin
-rw-r--r-- 1 admin admin 807 Nov 7 2023 .profile drwx------ 2 admin admin 4096 Nov 7 2023 .ssh
-rw-r--r-- 1 admin admin 208 Nov 7 19:32 .wget-hsts
-rw------- 1 admin admin 116 Nov 7 19:41 .Xauthority
## Usando um Segundo Disco para Armazenar a Blockchain (opcional) ...
## 1. Eliminar a ligação simbólica criada com falha Tente criar novamente a ligação simbólica
## 1. Verifique se a ligação simbólica foi criada corretamente desta vez e se tem agora o resultado esperado: .bitcoin -> /mnt/blockchain/bitcoin Elimine a pasta bitcoin antiga Reinicie novamente o serviço bitcoin.
Pode acompanhar a evolução da execução do bitcoin.
Depois de confirmado que atingiu o estado de progress=1.000000 poderá
reiniciar os restantes serviços de volta. Reinicie os serviços que tiver interesse
```bash sudo rm -r .bitcoin
``` ln -s /mnt/blockchain/bitcoin /home/admin/.bitcoin ls -la
```bash sudo rm -r /data/bitcoin
```
```bash sudo systemctl enable bitcoind.service
```
```bash sudo systemctl restart bitcoind
``` journalctl -fu bitcoind
```bash $ sudo systemctl enable lnd.service
```
```bash $ sudo systemctl start lnd
```
```bash $ sudo systemctl enable btcrpcexplorer.service
```
```bash $ sudo systemctl start btcrpcexplorer
```
```bash $ sudo systemctl enable electrs.service
```
```bash $ sudo systemctl start electrs
```
## Usando um Segundo Disco para Armazenar a Blockchain (opcional) ...
Anterior
## Instalação Bitcoin Core Próximo
# Upgrade
 Atualizado há 7 meses
## Usando um Segundo Disco para Armazenar a Blockchain (opcional) ...
