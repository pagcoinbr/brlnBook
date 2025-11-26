# Upgrade
 Knots
Confira a última versão na página oficial do Bitcoin Knots Para este guia, utilizaremos a versão Linux x8664.
Entre como e mude para o diretório temporário:
Crie a variável temporária:
Baixe os arquivos necessários para validação e instalação:
```bash cd /tmp
``` VERSION=29.2.knots
```bash wget https://bitcoinknots.org/files/29.x/$VERSION/bitcoin-```
```bash $VERSION-x86_64-linux-gnu.tar.gz
```
```bash wget https://bitcoinknots.org/files/29.x/$VERSION/SHA256SUMS```
```bash wget https://bitcoinknots.org/files/29.x/$VERSION/SHA256SUMS.asc```
```bash wget https://bitcoinknots.org/files/29.x/$VERSION/SHA256SUMS.ots``` sha256sum --ignore-missing --check SHA256SUMS
As chaves estão disponíveis no repositório oficial do Bitcoin Knots:
Verifique se o arquivo de checksums está assinado
## usando as chaves de assinatura oficiais.
O comando acima exibirá as verificações de assinatura para cada uma das chaves públicas que assinaram o arquivo.
```bash bitcoin-29.2.knots20251010-x86_64-linux-gnu.tar.gz: OK
```
```bash curl -s "https://api.github.com/repos/bitcoinknots/```
```bash bitcoinknots.github.io/contents/keys" \
``` | grep download_url | grep -oE "https://[a-zA-Z0-9./_-]+"| while
read url; do curl -s "$url" | gpg --import; done gpg: key 17565732E08E5E41: public key "Luke Dashjr <luke@dashjr.org>" imported gpg: Total number processed:
gpg: imported:
gpg --verify SHA256SUMS.asc SHA256SUMS gpg: Good signature from ...
Primary key fingerprint: ...
Agora, basta verificar se a está próxima da da versão que você está instalando.
Se tiver esta saída:
Isso significa que o carimbo de tempo está blockchain do Bitcoin.
Você pode para que a confirmação seja feita.
se você já verificou o e a corretamente.
ots --no-cache verify SHA256SUMS.ots -f SHA256SUMS Got 1 attestation(s) from https://btc.calendar.catallaxy.comGot 1 attestation(s) from https://finney.calendar.eternitywall.comGot 1 attestation(s) from https:// bob.btc.calendar.opentimestamps.org Got 1 attestation(s) from https://
alice.btc.calendar.opentimestamps.org Success! Bitcoin block 862491 attests existence as of 2025-10-UTC Calendar https://btc.calendar.catallaxy.com:Pending confirmation in Bitcoin blockchain Calendar https://finney.calendar.eternitywall.com:Pending confirmation in Bitcoin blockchain Calendar https://bob.btc.calendar.opentimestamps.org:Pending confirmation in Bitcoin blockchain Calendar https://alice.btc.calendar.opentimestamps.org:Pending confirmation in Bitcoin blockchain tar -xzvf bitcoin-$VERSION-x86_64-linux-gnu.tar.gz
```bash sudo install -m 0755 -o root -g root -t /usr/local/bin bitcoin-
```
```bash $VERSION/bin/bitcoin-cli bitcoin-$VERSION/bin/bitcoind
```
```bash bitcoin-cli --version
``` Bitcoin Knots RPC client version v29.2.knots Copyright (C) 2009-The Bitcoin Knots developers
```bash sudo rm -r bitcoin-$VERSION && sudo rm bitcoin-$VERSION-x86_64-
``` linux-gnu.tar.gz && sudo rm SHA256SUMS && sudo rm SHA256SUMS.asc && sudo rm SHA256SUMS.ots
```bash sudo systemctl restart bitcoind
``` O Bitcoin Knots é um fork do Bitcoin Core mantido por , contendo melhorias e opções de privacidade avançadas.
A instalação e atualização seguem o mesmo fluxo de segurança do Core,
garantindo integridade e autenticidade por meio das assinaturas GPG e dos carimbos de tempo na blockchain.
Anterior
# Upgrade
 Próximo
# Instalação
 do LND Atualizado há 1 mês
