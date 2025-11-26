# Instalação
 Thunderhub (opcional)
ThunderHub é um gestor de nós LND de código aberto onde pode gerir e
monitorizar o seu nó em qualquer dispositivo ou navegador. Permite-lhe
assumir o controlo da rede lightning com um UX simples e intuitivo e a pilha de tecnologia mais actualizada.
- Bitcoin Core
## • LND
- Outros ◦Node + NPM
O Node + NPM também está indicado aqui neste tutorial para o BTC RPC Explorer
- Com o usuário admin , verifique a versão do Node do resultado esperado:
- Verificar a versão do NPM do resultado esperado:
Definir uma variável de ambiente de versão temporária para a instalação
- Importar a chave GPG do programador node -v > v16.14.
npm -v > 8.19.
## VERSION=0.13.
```bash curl https://github.com/apotdevin.gpg| gpg --import
```
- Faça o download do código-fonte diretamente do GitHub, selecione o
ramo de lançamento mais recente associado e vá para a pasta thunderhub
- Verificar a versão do resultado esperado:
- Instalar todas as dependências e os módulos necessários utilizando o
NPM o comando npm audit fix , que pode quebrar o código original!!! Example of expected output
```bash git clone --branch v$VERSION https://github.com/apotdevin/``` thunderhub.git && cd thunderhub
```bash git verify-commit v$VERSION
``` gpg: Signature made Fri May 26 16:56:42 2023 CEST gpg: using RSA key
## 3C8A01A8344B66E7875CE5534403F1DFBE gpg: Good signature from "Anthony Potdevin <potdevin.anthony@gmail.com>" [unknown]
gpg: WARNING: This key is not certified with a trusted signature!
gpg: There is no indication that the signature belongs to the owner.
Primary key fingerprint: 3C8A 01A8 344B 66E7 875C E553 4403 F1DF
## BE77 npm install npm warn deprecated @types/cron@2.4.0: This is a stub types
definition. cron provides its own type definitions, so you do not need this installed.
npm warn deprecated stringify-package@1.0.1: This module is not used anymore, and has been replaced by @npmcli/package-json
npm warn deprecated @babel/plugin-proposal-class-properties@7.18.6: This proposal has been merged to the ECMAScript
standard and thus this plugin is no longer maintained. Please use @babel/plugin-transform-class -properties instead.
npm warn deprecated apollo-datasource@3.3.2: The `apollo-datasource` package is part of Apollo Server v2 and v3, which are now deprecated (end-of-life October 22nd 2023 and October 22nd 2024, respectively). See https://www.apollographql.com/docs/apollo-server/previous-versions/ for more details.
npm warn deprecated apollo-server-plugin-base@3.7.2: The `apollo-server-plugin-base` package is part of Apollo Server v2 and v3, which are now deprecated (end-of-life October 22nd 2023 and October 22nd 2024, respectively). This package's functionality is now found in the `@apollo/server` package. See https:// more details.
npm warn deprecated apollo-server-types@3.8.0: The `apollo-server-types` package is part of Apollo Server v2 and v3, which are now deprecated (end-of-life October 22nd 2023 and October 22nd 2024, respectively). This package's functionality is now found in the `@apollo/server` package. See https://www.apollographql.com/docs/apollo-server/previous-versions/ for more details.
npm warn deprecated apollo-server-errors@3.3.1: The `apollo-server-errors` package is part of Apollo Server v2 and v3, which
are now deprecated (end-of-life October 22nd 2023 and October 22nd 2024, respectively). This package's functionality is now found in the `@apollo/server` package. See https://www.apollographql.com/docs/apollo-server/previous-versions/ for more details.
npm warn deprecated @babel/plugin-proposal-object-rest-spread@7.20.7: This proposal has been merged to the ECMAScript
standard and thus this plugin is no longer maintained. Please use @babel/plugin-transform-object-rest-spread instead.
npm warn deprecated @apollo/server-plugin-landing-page-graphql-playground@4.0.0: The use of GraphQL Playground in Apollo Server
was supported in previous versions, but this is no longer the case
as of December 31, 2022. This package exists for v4 migration
purposes only. We do not intend to resolve security issues or
other bugs with this package if they arise, so please migrate away from this to [Apollo Server's default Explorer](https:// as soon as possible as soon as possible.
npm warn deprecated apollo-server-env@4.2.1: The `apollo-server-env` package is part of Apollo Server v2 and v3, which are now deprecated (end-of-life October 22nd 2023 and October 22nd 2024, respectively). This package's functionality is now found in the `@apollo/utils.fetcher` package. See https:// more details.
npm warn deprecated apollo-reporting-protobuf@3.4.0: The `apollo-reporting-protobuf` package is part of Apollo Server v2 and v3, which are now deprecated (end-of-life October 22nd 2023 and October 22nd 2024, respectively). This package's functionality is now found in the `@apollo/usage-reporting-protobuf` package. See versions/ for more details.
npm warn deprecated subscriptions-transport-ws@0.11.0: The `subscriptions-transport-ws` package is no longer maintained. We recommend you use `graphql-ws` instead. For help migrating Apollo software to `graphql-ws`, see https://www.apollographql.com/docs/apollo-server/data/subscriptions/#switching-from-subscriptions-transport-ws For general help using `graphql-ws`, see https://
```bash github.com/enisdenjo/graphql-ws/blob/master/README.md
``` > thunderhub@0.13.32 prepare > husky install husky - Git hooks installed added 1949 packages, and audited 1950 packages in 46s 251 packages are looking for funding run `npm fund` for details 23 vulnerabilities (2 low, 6 moderate, 15 high)
To address issues that do not require attention, run:
npm audit fix To address all issues (including breaking changes), run:
npm audit fix --force Run `npm audit` for details.
npm notice
npm notice New patch version of npm available! 10.8.1 -> 10.8.
npm notice Changelog: https://github.com/npm/cli/releases/tag/v10.8.
npm notice To update run: npm install -g npm@10.8.
npm notice Melhore a sua privacidade optando por não utilizar Next.js
[telemetria] Telemetry | Next.js by Vercel - The React Framework Resultado esperado:
npx next telemetry disable Your preference has been saved to /home/thunderhub/.config/ nextjs-nodejs/config.json.
Status: Disabled You have opted-out of Next.js' anonymous telemetry program.
No data will be collected from your machine.
Learn more: https://nextjs.org/telemetry- Construir do resultado esperado npm run build > thunderhub@0.13.32 prebuild > rimraf dist && rimraf .next > thunderhub@0.13.32 build > npm run build:nest && npm run build:next > thunderhub@0.13.32 build:nest > nest build > thunderhub@0.13.32 build:next > cd src/client && next build
./src/components/chart/BarChart.tsx 61:6 Warning: React Hook useMemo has a missing dependency:
'dataKey'. Either include it or remove the dependency array.
react-hooks/exhaustive-deps ./src/components/chart/HorizontalBarChart.tsx 139:6 Warning: React Hook useMemo has a missing dependency:
'maxValue'. Either include it or remove the dependency array.
react-hooks/exhaustive-deps ./src/components/table/DebouncedInput.tsx 30:6 Warning: React Hook useEffect has missing dependencies:
'debounce' and 'onChange'. Either include them or remove the
dependency array. If 'onChange' changes too often, find the parent
component that defines it and wrap that definition in useCallback.
react-hooks/exhaustive-deps info - Need to disable some ESLint rules? Learn more here:
✓ Linting and checking validity of types Browserslist: caniuse-lite is outdated. Please run:
npx browserslist@latest --update-db Why you should do it regularly: https://github.com/browserslist/browserslist#browsers-data-updating ✓ Creating an optimized production build ✓ Compiled successfully ✓ Collecting page data ✓ Collecting build traces ✓ Finalizing page optimization Route (pages)
Size First Load JS Route (pages) Size First Load JS ┌ λ / 23.9 kB 557 kB ├ /_app 0 B 243 kB ├ λ /404 344 B 243 kB ├ λ /amboss 3.92 kB 250 kB ├ λ /chain 5.69 kB 265 kB ├ λ /channels 6.61 kB 310 kB ├ λ /channels/[slug] 4.44 kB 250 kB ├ λ /chat 6.63 kB 255 kB ├ λ /dashboard 586 B 247 kB ├ λ /forwards 23.5 kB 545 kB ├ λ /leaderboard 3.62 kB 281 kB ├ λ /lnmarkets 5.2 kB 248 kB ├ λ /login 5.54 kB 249 kB ├ λ /peers 6.29 kB 265 kB ├ λ /rebalance 9.28 kB 287 kB ├ λ /settings 8.66 kB 257 kB ├ λ /settings/dashboard 458 B 247 kB ├ λ /sso 2.78 kB 246 kB ├ λ /stats 7.02 kB 253 kB ├ λ /swap 11.2 kB 289 kB ├ λ /tools 7.38 kB 250 kB └ λ /transactions 5.08 kB 523 kB + First Load JS shared by all 247 kB ├ chunks/framework-80ea8c0f440c6a32.js 45.4 kB ├ chunks/main-5aa2e2aecccdc7ca.js 33 kB ├ chunks/pages/_app-43ed1c524f6479ab.js 162 kB ├ chunks/webpack-bafa1815dd7342f2.js 2.17 kB └ css/9f506b76c3634369.css 4.22 kB λ (Server) server-side renders at runtime (uses getInitialProps or getServerSideProps)
- Verifique se a instalação está correta, solicitando a versão do resultado esperado:
head -n 3 /home/admin/thunderhub/package.json | grep version > "version": "0.13.32",
- Copiar o modelo do ficheiro de configuração
- Editar o ficheiro de configuração
- Editar a linha seguinte para que coincida com a seguinte. Guardar e sair
- Criar um novo ficheiro thubConfig.yaml
- Copiar e colar as informações seguintes
Substitua a **[E]** ThunderHub password pela sua, mantendo as aspas [' '] Pode pré-ativar o ping automático de healthchecks e/ou
backups de canais para o Amboss antes de iniciar o ThunderHub, adicionando algumas linhas Ativar as cópias de segurança automáticas:
cp .env .env.local
```bash nano .env.local
``` ACCOUNT_CONFIG_PATH='/home/admin/thunderhub/thubConfig.yaml'
```bash nano thubConfig.yaml
``` masterPassword: 'PASSWORD' accounts:
- name: 'MiniBolt' serverUrl: '127.0.0.1:10009' macaroonPath: '/data/lnd/data/chain/bitcoin/mainnet/ admin.macaroon' certificatePath: '/data/lnd/tls.cert' password: '**[E]** ThunderHub password' backupsEnabled: true Ativar os controlos de healthcheck automáticos:
De qualquer forma, é possível ativar esta opção mais tarde utilizando a interface ThunderHub, que será explicada na secção adicional Ativar
cópias de segurança automáticas e notificações de verificação do estado de saúde
Lembre-se de que, se você parar o ThunderHub, o Amboss interpretará
que seu nó está offline porque a conexão é estabelecida entre o
ThunderHub <> Amboss para enviar pings de verificação de integridade
- Criar o ficheiro de serviço
- Colar a seguinte configuração. Guardar e sair healthCheckPingEnabled: true
```bash sudo nano /etc/systemd/system/thunderhub.service
```
- Ativar o arranque automático
- Preparar a monitorização do "thunderhub" pelo diário do systemd e
verificar a saída do registo. Você pode sair do monitoramento a qualquer momento com Ctrl-C
# BRLN
 Bolt: unidade systemd para Thunderhub
# /etc/systemd/system/thunderhub.service [Unit] Description=ThunderHub Requires=lnd.service After=lnd.service [Service] WorkingDirectory=/home/admin/thunderhub ExecStart=/usr/bin/npm run start User=admin Group=admin
# Process
 management
#################### TimeoutSec=
# Hardening
 Measures
#################### PrivateTmp=true ProtectSystem=full NoNewPrivileges=true PrivateDevices=true [Install] WantedBy=multi-user.target
```bash sudo systemctl enable thunderhub
``` journalctl -fu thunderhub
Para ficar de olho nos movimentos do software, inicie seu programa SSH
direto (por exemplo, PuTTY) uma segunda vez, conecte-se ao nó MiniBolt e faça login como "admin"
- Iniciar o serviço da saída esperada no primeiro terminal com journalctl -fu thunderhub
```bash sudo systemctl start thunderhub
``` Jun 28 23:35:43 minibolt npm[513274]: > thunderhub@0.13.15 start Jun 28 23:35:43 minibolt npm[513274]: > cross-env NODE_ENV=production nest start Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [NestFactory] Starting Nest application...
Jun 28 23:35:53 minibolt npm[513313]: Getting production env variables.
Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] AppModule dependencies initialized +82ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] PassportModule dependencies initialized +1ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] LndModule dependencies initialized +0ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] ApiModule dependencies initialized +0ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] MainModule dependencies initialized +0ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] DiscoveryModule dependencies initialized +1ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] ConfigHostModule dependencies initialized +0ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] ScheduleModule dependencies initialized +1ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] ConfigModule dependencies initialized +1ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] ConfigModule dependencies initialized +0ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] ThrottlerModule dependencies initialized +4ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] JwtModule dependencies initialized +0ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] ViewModule dependencies initialized +1ms Jun 28 23:35:53 minibolt npm[513313]: [Nest]
06/28/ Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] GraphQLSchemaBuilderModule dependencies initialized +0ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] WinstonModule dependencies initialized +1ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] FilesModule dependencies initialized +0ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] FetchModule dependencies initialized +0ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] AuthenticationModule dependencies initialized +0ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] AccountsModule dependencies initialized +1ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] BaseModule dependencies initialized +0ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] BitcoinModule dependencies initialized +1ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] GithubModule dependencies initialized +0ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] UserConfigModule dependencies initialized +0ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] AuthenticationModule dependencies initialized +1ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] AccountModule dependencies initialized +0ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] NodeModule dependencies initialized +0ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] BosModule dependencies initialized +0ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] GraphQLModule dependencies initialized +1ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] WsModule dependencies initialized +1ms Jun 28 23:35:53 minibolt npm[513313]: [Nest]
- 06/28/ Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 06/28/2023, 11:35:53 PM LOG [InstanceLoader] WalletModule dependencies initialized +0ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] ToolsModule dependencies initialized +0ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] MacaroonModule dependencies initialized +0ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] NetworkModule dependencies initialized +0ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] PeerModule dependencies initialized +1ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] ChainModule dependencies initialized +0ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] EdgeModule dependencies initialized +0ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] ChannelsModule dependencies initialized +0ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] ForwardsModule dependencies initialized +1ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] HealthModule dependencies initialized +0ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] TransactionsModule dependencies initialized +0ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] InvoicesModule dependencies initialized +0ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] ChatModule dependencies initialized +0ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] BoltzModule dependencies initialized +1ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] NodeModule dependencies initialized +0ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] AuthModule dependencies initialized +0ms Jun 28 23:35:53 minibolt npm[513313]: [Nest]
- 06/28/2023, Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 06/28/2023, 11:35:53 PM LOG [InstanceLoader] LnUrlModule dependencies initialized +0ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] AmbossModule dependencies initialized +1ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] SubModule dependencies initialized +0ms Jun 28 23:35:53 minibolt npm[513313]: [Nest] 513313 - 06/28/2023, 11:35:53 PM LOG [InstanceLoader] LnMarketsModule dependencies initialized +0ms Jun 28 23:35:53 minibolt npm[513313]: { Jun 28 23:35:53 minibolt npm[513313]: message: 'WS server created', Jun 28 23:35:53 minibolt npm[513313]: level: 'info', Jun 28 23:35:53 minibolt npm[513313]: timestamp:
## '2023-06-28T21:35:53.547Z' Jun 28 23:35:53 minibolt npm[513313]: } Jun 28 23:35:53 minibolt npm[513313]: { Jun 28 23:35:53 minibolt npm[513313]: context: 'RoutesResolver', Jun 28 23:35:53 minibolt npm[513313]: level: 'info', Jun 28 23:35:53 minibolt npm[513313]: message: 'ViewController {/}:', Jun 28 23:35:53 minibolt npm[513313]: timestamp:
## '2023-06-28T21:35:53.552Z' Jun 28 23:35:53 minibolt npm[513313]: } Jun 28 23:35:53 minibolt npm[513313]: { Jun 28 23:35:53 minibolt npm[513313]: context: 'RouterExplorer', Jun 28 23:35:53 minibolt npm[513313]: level: 'info', Jun 28 23:35:53 minibolt npm[513313]: message: 'Mapped {/, GET} route', Jun 28 23:35:53 minibolt npm[513313]: timestamp:
## '2023-06-28T21:35:53.555Z' Jun 28 23:35:53 minibolt npm[513313]: } Jun 28 23:35:53 minibolt npm[513313]: { Jun 28 23:35:53 minibolt npm[513313]: context: 'RouterExplorer', Jun 28 23:35:53 minibolt npm[513313]: level: 'info', Jun 28 23:35:53 minibolt npm[513313]: message: 'Mapped {/*, GET} route', Jun 28 23:35:53 minibolt npm[513313]: timestamp:
## '2023-06-28T21:35:53.555Z' Jun 28 23:35:53 minibolt npm[513313]: } Jun 28 23:35:53 minibolt npm[513313]: { Jun 28 23:35:53 minibolt npm[513313]: message: 'Server accounts that will be available: MiniBolt', Jun 28 23:35:53 minibolt npm[513313]: level: 'info', Jun 28 23:35:53 minibolt npm[513313]: timestamp:
## '2023-06-28T21:35:53.563Z' Jun 28 23:35:53 minibolt npm[513313]: } Jun 28 23:35:54 minibolt npm[513313]: Persisted queries are
enabled and are using an unbounded cache. Your server is
vulnerable to denial of service attacks via memory exhaustion. Set `cache: "bounded"` or `persistedQueries: false` in your ApolloServer constructor, or see https://go.apollo.dev/s/cache-backendsfor other alternatives.
Jun 28 23:35:54 minibolt npm[513313]: { Jun 28 23:35:54 minibolt npm[513313]: context: 'GraphQLModule', Jun 28 23:35:54 minibolt npm[513313]: level: 'info', Jun 28 23:35:54 minibolt npm[513313]: message: 'Mapped {/ graphql, POST} route', Jun 28 23:35:54 minibolt npm[513313]: timestamp:
## '2023-06-28T21:35:54.092Z' Jun 28 23:35:54 minibolt npm[513313]: } Jun 28 23:35:54 minibolt npm[513313]: { Jun 28 23:35:54 minibolt npm[513313]: context:
'NestApplication', Jun 28 23:35:54 minibolt npm[513313]: level: 'info', Jun 28 23:35:54 minibolt npm[513313]: message: 'Nest application successfully started', Jun 28 23:35:54 minibolt npm[513313]: timestamp:
## '2023-06-28T21:35:54.524Z' Jun 28 23:35:54 minibolt npm[513313]: } Jun 28 23:35:54 minibolt npm[513313]: Application is running on:
Jun 28 23:35:54 minibolt npm[513313]: (node:513313) [DEP0123]
DeprecationWarning: Setting the TLS ServerName to an IP address is
not permitted by RFC 6066. This will be ignored in a future version.
Jun 28 23:35:54 minibolt npm[513313]: (Use `node --trace-deprecation ...` to show where the warning was created)
[...] Agora aponte o seu browser para http://minibolt.local:3000 ou página inicial do ThunderHub
- Certifique-se de que o serviço está funcionando e escutando no porto padrão 3000 e no porto HTTPS
```bash sudo ss -tulpn | grep -v 'dotnet' | grep 'LISTEN.*\(4002\|3000\)'
``` Resultado esperado:
Parabéns**! Tem agora uma aplicação Web de gestão de nós LND Thunderhub em funcionamento A atualização para uma [nova versão] (https://github.com/apotdevin/thunderhub/releases) deve ser simples.
- Parar o serviço
- Ir para a pasta thunderhub
- Definir a versão da variável de ambiente
- Puxar as alterações do GitHub Exemplo de resultados esperados > tcp LISTEN 0 511 0.0.0.0:4002 0.0.0.0:* users:(("nginx",pid=992796,fd=7),("nginx",pid=992795,fd=7), ("nginx",pid=992794,fd=7),("nginx",pid=992793,fd=7), ("nginx",pid=992792,fd=7)) > tcp LISTEN 0 511 *:3000 *:* users:(("next-router-wor",pid=1405797,fd=32))
```bash sudo systemctl stop thunderhub
```
```bash cd thunderhub
```
## VERSION=0.13.
```bash git pull https://github.com/apotdevin/thunderhub.gitv$VERSION
```
- Instalar todos os módulos necessários Example of expected output From https://github.com/apotdevin/thunderhub- tag v0.13.28 -> FETCH_HEAD Updating 1d5a3fe5..5e9b3f Fast-forward CHANGELOG.md | 7 +++++++ package-lock.json | 4 ++--
package.json | 2 +-
src/server/modules/api/amboss/amboss.gql.ts | 9 +++++++++ src/server/modules/api/amboss/amboss.service.ts | 16 +++++++++++ +++++ src/server/modules/sub/sub.service.ts | 113 +++++++++++ ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++ ++++++++++++++++++++++++++++++++++++ 6 files changed, 148 insertions(+), 3 deletions(-)
npm install npm WARN deprecated subscriptions-transport-ws@0.11.0: The `subscriptions-transport-ws` package is no longer maintained. We recommend you use `graphql-ws` instead. For help migrating Apollo software to `graphql-ws`, see https://www.apollographql.com/docs/apollo-server/data/subscriptions/#switching-from-subscriptions-transport-ws For general help using `graphql-ws`, see https://
```bash github.com/enisdenjo/graphql-ws/blob/master/README.md
``` npm WARN deprecated apollo-server-plugin-base@3.7.2: The `apollo-server-plugin-base` package is part of Apollo Server v2 and v3, which are now deprecated (end-of-life October 22nd 2023). This package's functionality is now found in the `@apollo/server` package. See https://www.apollographql.com/docs/apollo-server/previous-versions/ for more details.
npm WARN deprecated apollo-server-types@3.8.0: The `apollo-server-types` package is part of Apollo Server v2 and v3, which are now deprecated (end-of-life October 22nd 2023). This package's functionality is now found in the `@apollo/server` package. See versions/ for more details.
npm WARN deprecated apollo-server-express@3.12.0: The `apollo-server-express` package is part of Apollo Server v2 and v3, which are now deprecated (end-of-life October 22nd 2023). This package's functionality is now found in the `@apollo/server` package. See versions/ for more details.
npm WARN deprecated apollo-server@3.12.0: The `apollo-server`
package is part of Apollo Server v2 and v3, which are now deprecated (end-of-life October 22nd 2023). This package's functionality is now found in the `@apollo/server` package. See versions/ for more details.
npm WARN deprecated apollo-reporting-protobuf@3.4.0: The `apollo-reporting-protobuf` package is part of Apollo Server v2 and v3, which are now deprecated (end-of-life October 22nd 2023). This
package's functionality is now found in the `@apollo/usage-reporting-protobuf` package. See https://www.apollographql.com/docs/apollo-server/previous-versions/ for more details.
npm WARN deprecated apollo-server-core@3.12.0: The `apollo-server-core` package is part of Apollo Server v2 and v3, which are now deprecated (end-of-life October 22nd 2023). This package's functionality is now found in the `@apollo/server` package. See versions/ for more details.
(#################⠂) ⠧ reify:value-or-promise: timing reifyNode:node_modules/foreground-child/node_modules/signal-exit Completed in 39393ms [...] > thunderhub@0.13.19 prepare > husky install husky - Git hooks installed added 1879 packages, and audited 1880 packages in 1m 201 packages are looking for funding run `npm fund` for details 16 vulnerabilities (1 low, 5 moderate, 10 high)
To address all issues, run:
npm audit fix Run `npm audit` for details.
npm notice
npm notice New minor version of npm available! 9.5.1 -> 9.8.
npm notice Changelog: https://github.com/npm/cli/releases/tag/v9.8.
npm notice Run npm install -g npm@9.8.0 to update!
npm notice
- Construir Exemplo de resultados esperados npm run build > thunderhub@0.13.24 prebuild > rimraf dist && rimraf .next > thunderhub@0.13.24 build > npm run build:nest && npm run build:next > thunderhub@0.13.24 build:nest > nest build > thunderhub@0.13.24 build:next > cd src/client && next build
./src/components/chart/BarChart.tsx 61:6 Warning: React Hook useMemo has a missing dependency:
'dataKey'. Either include it or remove the dependency array.
react-hooks/exhaustive-deps ./src/components/chart/HorizontalBarChart.tsx 139:6 Warning: React Hook useMemo has a missing dependency:
'maxValue'. Either include it or remove the dependency array.
react-hooks/exhaustive-deps ./src/components/table/DebouncedInput.tsx 30:6 Warning: React Hook useEffect has missing dependencies:
'debounce' and 'onChange'. Either include them or remove the
dependency array. If 'onChange' changes too often, find the parent
component that defines it and wrap that definition in useCallback.
react-hooks/exhaustive-deps info - Need to disable some ESLint rules? Learn more here:
✓ Linting and checking validity of types ▲ Next.js 14.0.
Browserslist: caniuse-lite is outdated. Please run:
npx browserslist@latest --update-db Why you should do it regularly: https://github.com/browserslist/browserslist#browsers-data-updating ✓ Creating an optimized production build ✓ Compiled successfully ✓ Collecting page data ✓ Collecting build traces ✓Finalizing page optimization ✓ Finalizing page optimization Route (pages) Size First Load JS ┌ λ / 23.8 kB 561 kB ├ /_app 0 B 246 kB ├ λ /404 344 B 246 kB ├ λ /amboss 3.31 kB 252 kB ├ λ /chain 5.73 kB 268 kB ├ λ /channels 6.75 kB 312 kB ├ λ /channels/[slug] 4.47 kB 253 kB ├ λ /chat 6.76 kB 259 kB ├ λ /dashboard 586 B 250 kB ├ λ /forwards 24.1 kB 550 kB ├ λ /leaderboard 3.62 kB 283 kB ├ λ /lnmarkets 5.22 kB 251 kB ├ λ /login 5.6 kB 252 kB ├ λ /peers 6.3 kB 269 kB ├ λ /rebalance 9.45 kB 289 kB ├ λ /settings 8.73 kB 260 kB ├ λ /settings/dashboard 458 B 250 kB ├ λ /sso 2.79 kB 249 kB ├ λ /stats 7.18 kB 256 kB ├ λ /swap 11.4 kB 291 kB ├ λ /tools 7.46 kB 253 kB └ λ /transactions 5.09 kB 527 kB + First Load JS shared by all 250 kB ├ chunks/framework-1ebad0ea60aef44d.js 45.7 kB ├ chunks/main-f884d18fd3231f30.js 33.2 kB ├ chunks/pages/_app-23ed15c0ff29868f.js 165 kB ├ chunks/webpack-9d8d1d250efc304b.js 2.17 kB └ css/ba8e388a301f6e52.css 3.78 kB λ (Dynamic) server-rendered on demand using Node.js
- Verificar a atualização correta do resultado esperado:
- Iniciar novamente o serviço head -n 3 /home/admin/thunderhub/package.json | grep version > "version": "0.13.20",
- Parar o thunderhub
- Desativar o arranque automático (se ativado)
- Eliminar o serviço
- Comentar ou remover as linhas de serviço ocultas do ThunderHub no torrc. Guardar e sair
- Recarregar a configuração do tor para aplicar as alterações
```bash sudo systemctl start thunderhub
```
```bash sudo systemctl stop thunderhub
```
```bash sudo systemctl disable thunderhub
```
```bash sudo rm /etc/systemd/system/thunderhub.service
```
```bash sudo nano +63 /etc/tor/torrc --linenumbers
```
# Hidden
 Service Thunderhub
#HiddenServiceDir /var/lib/tor/hidden_service_thunderhub/
#HiddenServiceVersion
#HiddenServicePoWDefensesEnabled
#HiddenServicePort 80 127.0.0.1:
```bash sudo systemctl reload tor
``` Anterior
## Instalação LNDg Próximo
## BTCPay Server (opcional)
Atualizado há 4 meses
