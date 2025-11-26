# Upgrade

# Upgrade do Bitcoin Core Confira a última versão na GitHub page do projeto Bitcoin Core. Troque a
variável de ambiente "VERSION=x.xx" para o valor da última versão caso já não seja a desse guia.
- Entre como admin user e mude para o diretório temporário
- Crie a variável temporária
- Bitcoin Core
- Faça o Download do Binário, checksum, signature, e timestamp para o Bitcoin Core
```bash cd /tmp
```
## VERSION=29.
```bash wget https://bitcoincore.org/bin/bitcoin-core-$VERSION/bitcoin-```
```bash $VERSION-x86_64-linux-gnu.tar.gz
```
```bash wget https://bitcoincore.org/bin/bitcoin-core-$VERSION/SHA256SUMS```
```bash wget https://bitcoincore.org/bin/bitcoin-core-$VERSION/``` SHA256SUMS.asc
```bash wget https://bitcoincore.org/bin/bitcoin-core-$VERSION/``` SHA256SUMS.ots
- Verify the new version against its checksums Saída Esperada:
- Verifique se o arquivo de checksums está assinado criptograficamente
## usando as chaves de assinatura da versão (release signing keys).
O seguinte comando exibe as verificações de assinatura para cada uma das chaves públicas que assinaram o arquivo de checksums.
- Verifique se pelo menos algumas das assinaturas exibem o seguinte texto.
sha256sum --ignore-missing --check SHA256SUMS
```bash bitcoin-29.1-x86_64-linux-gnu.tar.gz: OK
```
```bash curl -s "https://api.github.com/repositories/355107265/contents/``` builder-keys" | grep download_url | grep -oE "https://[a-zA-Z0-9./-]+"| while read url; do curl -s "$url" | gpg --import;
done gpg: key 17565732E08E5E41: 29 signatures not checked due to missing keys gpg: /home/admin/.gnupg/trustdb.gpg: trustdb created gpg: key 17565732E08E5E41: public key "Andrew Chow <andrew@achow101.com>" imported gpg: Total number processed:
gpg: imported:
gpg: no ultimately trusted keys found [...] gpg --verify SHA256SUMS.asc SHA256SUMS gpg: Good signature from ...
Primary key fingerprint: ...
A saída a seguir é apenas um exemplo de uma das versões:
- Agora, basta verificar se a data do carimbo de tempo (timestamp) está
próxima da data de lançamento da versão que você está instalando.
Se tiver essa saída
 Isso significa que o carimbo de tempo (timestamp) está pendente de confirmação na blockchain do Bitcoin.
Você pode pular esta etapa ou aguardar algumas horas/dias para realizar essa verificação.
É seguro pular essa etapa de verificação se você seguiu as anteriores e prosseguir para o próximo passo.
Se você estiver satisfeito com as verificações de , extraia os binários do ots --no-cache verify SHA256SUMS.ots -f SHA256SUMS Got 1 attestation(s) from https://btc.calendar.catallaxy.comGot 1 attestation(s) from https://finney.calendar.eternitywall.comGot 1 attestation(s) from https:// bob.btc.calendar.opentimestamps.org Got 1 attestation(s) from https://
alice.btc.calendar.opentimestamps.org Success! Bitcoin block 766964 attests existence as of 2022-12-UTC Calendar https://btc.calendar.catallaxy.com:Pending confirmation in Bitcoin blockchain Calendar https://finney.calendar.eternitywall.com:Pending confirmation in Bitcoin blockchain Calendar https://bob.btc.calendar.opentimestamps.org:Pending confirmation in Bitcoin blockchain Calendar https://alice.btc.calendar.opentimestamps.org:Pending confirmation in Bitcoin blockchain tar -xzvf bitcoin-$VERSION-x86_64-linux-gnu.tar.gz
- Faça a instalação
- Confirme a nova versão
A saída abaixo é somente um exemplo de versões passadas.
Apague os arquivos de instalação do diretório /tmp
- Reinicie o serviço do Bitcoin Anterior
## Usando um Segundo Disco para Armazenar a Blockchain (opcional)
Próximo
# Upgrade
 Knots Atualizado há 1 mês
```bash sudo install -m 0755 -o root -g root -t /usr/local/bin bitcoin-
```
```bash $VERSION/bin/bitcoin-cli bitcoin-$VERSION/bin/bitcoind
```
```bash bitcoin-cli --version
``` Bitcoin Core RPC client version v26.0.
Copyright (C) 2009-2022 The Bitcoin Core developers [...]
```bash sudo rm -r bitcoin-$VERSION && sudo rm bitcoin-$VERSION-x86_64-
``` linux-gnu.tar.gz && sudo rm SHA256SUMS && sudo rm SHA256SUMS.asc && sudo rm SHA256SUMS.ots
```bash sudo systemctl restart bitcoind
```
