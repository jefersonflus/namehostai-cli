# NameHost AI Agent

Agente de terminal da NameHost AI para trabalhar com projetos locais usando os modelos disponibilizados pelo gateway NameHost.

Este repositório distribui somente os artefatos prontos para uso. O código de desenvolvimento permanece no ambiente interno do projeto.

## Download

Acesse a [Release v0.1.8](https://github.com/jefersonflus/namehostai-cli/releases/tag/v0.1.8) ou a [página de Releases](https://github.com/jefersonflus/namehostai-cli/releases).

A versão publicada inclui pacotes Windows e macOS:

- `namehost-ai-cli-windows-x64.msi` ou `.zip` para Windows x64.
- `namehost-ai-cli-windows-arm64.msi` ou `.zip` para Windows ARM64.
- `namehost-ai-cli-darwin-arm64.zip` para macOS Apple Silicon.
- `namehost-ai-cli-darwin-x64.zip` para macOS Intel.

O MSI instala o comando `namehost` no PATH do usuário e aparece em Aplicativos instalados. O ZIP é portátil: extraia o conteúdo e adicione a pasta `bin` ao PATH.

## Instalação no macOS

Requer macOS 13 ou superior. Baixe o ZIP correspondente e o arquivo `.sha256` na Release.

Para Apple Silicon, execute na pasta do download:

```sh
shasum -a 256 -c namehost-ai-cli-darwin-arm64.zip.sha256
unzip namehost-ai-cli-darwin-arm64.zip -d namehost-ai
mkdir -p "$HOME/.local/bin"
install -m 755 namehost-ai/bin/namehost "$HOME/.local/bin/namehost"
export PATH="$HOME/.local/bin:$PATH"
namehost --version
namehost login --browser
```

Em Macs Intel, substitua `darwin-arm64` por `darwin-x64`. Adicione `export PATH="$HOME/.local/bin:$PATH"` ao `~/.zshrc` para manter o comando disponível em novos terminais. O Bun não precisa estar instalado.

Os pacotes não possuem assinatura de distribuição nem notarização. A compilação, as arquiteturas, as permissões Unix, as bibliotecas embutidas e os hashes foram conferidos em Windows; execução, login e atualização em um Mac ainda não foram testados.

## Login

Use `namehost login --browser` para entrar pelo navegador ou `namehost login` para ativação por dispositivo. O endereço e o código mostrados pelo agente devem ser aprovados no portal.

O agente recebe um token Bearer de sessão. A chave da conta escolhida durante a aprovação permanece no portal e não é enviada ao CLI.

## Gateway e modelos

O agente usa o gateway `https://ia.namehost.com.br` e o catálogo de modelos da conta. As rotas compatíveis são:

- `GET /v1/models`
- `POST /v1/messages`
- `POST /v1/chat/completions`
- `POST /v1/responses`

## Novidades da v0.1.8

- Corrige o encerramento da interface interativa no Windows: `Ctrl+C` e `/exit` retornam ao prompt sem fechar a janela do CMD.
- Evita que a consulta de capacidades do terminal apareça como `+q4d73` ao sair.
- Restaura a tela e os modos do console depois da limpeza dos recursos do CLI.

Os dois comandos de saída foram verificados no console tradicional do Windows x64, incluindo a execução de outro comando após o encerramento do agente. Os pacotes macOS e Windows ARM64 foram compilados e validados estruturalmente; execução nativa nessas plataformas permanece sem validação.

## Funcionalidades da v0.1.7 mantidas na v0.1.8

- `--effort` no agente, chat e TUI; `/effort` abre o seletor dentro da tela interativa (`/variants` também funciona). A escolha vale para as próximas mensagens e é salva por modelo; `Default` restaura o padrão do servidor.
- GPT Luna/Sol via Responses usam níveis validados no gateway. Sonnet 5, Opus 5.5 e Fable 5.1 via Messages oferecem `low`, `medium`, `high`, `xhigh`, `max` conforme a documentação Claude; a aplicação efetiva desses presets pelo gateway ainda não está confirmada. O catálogo v2 do servidor tem prioridade sobre os presets locais.
- O CLI respeita `max_output_tokens` publicado por modelo. `namehost models --json` mostra limites, protocolos e a origem dos níveis de effort.
- `namehost doctor`, `namehost devices` e `namehost models --offline` permitem diagnóstico, gestão de dispositivos e consulta do catálogo salvo. Inferência continua exigindo conexão ao gateway.
- Credenciais no cofre do sistema em Windows/macOS, rotação de refresh token serializada e limpeza local de login/cache mesmo se a revogação remota falhar. `namehost logout --local` limpa somente o estado local.
- Correções de instaladores, atualização e API local autenticada para o SDK.

Exemplos:

```sh
namehost agent --model gpt-6-sol --effort high "Analise este projeto"
namehost chat --model claude-sonnet-5 --effort medium
namehost doctor --json
namehost devices
```

## Atualizações

Execute `namehost update --check` para verificar uma nova versão. Em uma instalação MSI, `namehost update` baixa e valida o MSI, pede confirmação e inicia o Windows Installer depois que o agente encerra. No Windows ZIP, o executável é substituído após o encerramento do processo. No macOS, o atualizador instala o executável diretamente, preservando as configurações do usuário.

O atualizador verifica HTTPS, tamanho publicado e SHA-256. Cada release contém checksums dos pacotes publicados. As versões atuais são distribuídas diretamente pelo GitHub Releases e não dependem de loja de aplicativos.

## Verificação do download

No Windows, confira o hash publicado junto ao arquivo:

```powershell
Get-FileHash .\namehost-ai-cli-windows-x64.zip -Algorithm SHA256
```

Nunca publique tokens, cookies ou arquivos de sessão em issues, commits ou logs.

## Suporte

Abra uma issue informando a versão, a arquitetura do Windows e a mensagem de erro. Remova tokens e dados pessoais antes de enviar logs.

## Licença

Consulte os termos publicados junto à Release correspondente.
