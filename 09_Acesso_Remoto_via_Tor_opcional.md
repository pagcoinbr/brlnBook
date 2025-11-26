# Acesso Remoto via Tor (opcional)

O acesso remoto via Tor é útil para conectar aplicações como carteiras e outros serviços ao seu node. Também é necessário para configurar o serviço de Lightning Address da BRLN https://pay.br-ln.com

Faça login como usuário e configure o LND para permitir LND REST de qualquer lugar. Edite o arquivo lnd.conf

Adicione a próxima linha na seção [Application Options]. Salve e saia.

```bash
sudo nano /data/lnd/lnd.conf
```

Adicione a seguinte linha:

```
restlisten=0.0.0.0:8080
```

Reinicie o LND para aplicar as alterações.

```bash
sudo systemctl restart lnd
```

Certifique-se de que a porta proxy gRPC agora está vinculada ao host 0.0.0.0 em vez de 127.0.0.1.

Saída esperada:

```bash
sudo ss -tulpn | grep LISTEN | grep lnd | grep 8080
```

```
tcp LISTEN 0 4096 0.0.0.0:8080 0.0.0.0:* users:(("lnd",pid=774047,fd=32))
```

Configure o Firewall para permitir solicitações de entrada do LND REST.

Certifique-se de que está logado como usuário e adicione as seguintes linhas na seção "location hidden services", abaixo de ## This section is just for location-hidden services ## no arquivo. Salve e saia.

```bash
sudo nano /etc/tor/torrc
```

Adicione:

```
# Hidden Service LND REST
HiddenServiceDir /var/lib/tor/hidden_service_lnd_rest/
HiddenServiceVersion 3
HiddenServicePoWDefensesEnabled 1
HiddenServicePort 8080 127.0.0.1:8080
```

Recarregue a configuração do Tor e obtenha seu endereço de conexão.

```bash
sudo systemctl reload tor
```

```bash
sudo cat /var/lib/tor/hidden_service_lnd_rest/hostname
```

Exemplo de saída esperada:

```
abcdefg..............xyz.onion
```

## BTCPay Server (opcional)

## Instalação Balance of Satoshis (BOS) Atualizado há 1 ano
