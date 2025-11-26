# Instalação
 LNDg
## 1. Clonar o repositório:
## 2. Mude o diretório para o repositório:
## 3. Certifique-se de que tem o Python virtualenv instalado:
## 4. Configure um ambiente virtual Python 3
## 5. Instalar as dependências necessárias:
## 6. Instalar o Whitenoise para servir .css
## 8. Inicialize as configurações necessárias para o seu site Django:
## 9. O usuário de login inicial é lndg-admin , e a senha será gerada e armazenada em: data/lndg-admin.txt
## 10. Para testar, Execute o servidor utilizando um servidor de desenvolvimento Python:
## 11. Acesso o LNDg com o navegador
b. Em usuário digite lndg-admin e em senha que foi fornecida após o passo
## 12. Funcionando, vamos agora configurar como serviço, passo 13.
## 13. Executar o LNDg como Serviço
```bash git clone https://github.com/cryptosharks131/lndg.git```
```bash cd lndg
```
```bash sudo apt install virtualenv
``` virtualenv -p python3 .venv .venv/bin/pip3 install -r requirements.txt .venv/bin/pip3 install whitenoise .venv/bin/python3 initialize.py --whitenoise .venv/bin/python3 manage.py runserver 0.0.0.0:
Copie o conteúdo abaixo e pressione CTRL (control) + O para salvar e CTRL (control) + X para sair.
Passo 2  Configurar o controlador de backend para dados, rebalanceamento automático, dados de fluxo HTLC e p2p-trade-secrets
O ficheiro controller.py orquestra os serviços necessários para atualizar a
base de dados backend com a informação mais actualizada, reequilibrar
quaisquer canais com base nas definições do seu painel de controlo LNDg,
ouvir quaisquer eventos de falha no seu fluxo HTLC e servir os segredos comerciais p2p.
```bash sudo nano /etc/systemd/system/lndg.service
``` [Unit] Description=LNDG Service After=lnd.service Requires=lnd.service [Service] WorkingDirectory=/home/admin/lndg ExecStart=/home/admin/lndg/.venv/bin/python3 /home/admin/lndg/ manage.py runserver 0.0.0.0:
User=admin Group=admin Restart=on-failure Type=simple StandardError=syslog NotifyAccess=none [Install] WantedBy=multi-user.target
```bash sudo systemctl enable lndg.service
```
```bash sudo systemctl start lndg.service
``` ◦Opção 1  Instalação com script Bash: sudo bash systemd.sh ◦Opção 2  Instruções de configuração manual
## 1. Se você não está usando as configurações padrão para o LND ou
gostaria de rodar em uma rede diferente da mainnet , use as flags
corretas no passo 6 (veja initialize.py --help ) ou edite as variáveis diretamente em lndg/settings.py .
## 2. Não é possível executar o servidor de desenvolvimento fora do modo
DEBUG devido a problemas de arquivo estático. Para resolver isso, instale e configure o Whitenoise executando o seguinte comando:
.venv/bin/pip install whitenoise && rm lndg/settings.py && .venv/bin/python initialize.py -wn . (veja 6.
## 3. Você pode sempre atualizar o arquivo lndg/settings.py modificando-o diretamente ou executando novamente o script .venv/bin/python initialize.py <options> -f . (veja
## 4. Se planeia executar este site continuamente, é aconselhável configurar
um servidor Web adequado para o alojar (ver Nginx abaixo).
## 5. Pode gerir as suas credenciais de início de sessão a partir da página de administração, acessível em http:<your-hosting-lndg-ip:port>/lndg-admin .
## 6. Se tiver problemas para aceder ao sítio, certifique-se de que a firewall
está aberta na porta 8889, onde o LNDg está a ser executado.
Assista a playlist do Diego Kolling com 8 aulas de como gerir o seu node
## usando o LNDg Aula LNDG Diego Kolling - https://bit.ly/4dghstAnterior
# Instalação
 do LND Próximo
## Instalação Thunderhub (opcional)
Atualizado há 7 meses
