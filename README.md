# NameHost AI Agent

Agente de terminal da NameHost AI para trabalhar com projetos locais usando os modelos disponibilizados pelo gateway NameHost.

Este repositório distribui somente os artefatos prontos para uso. O código de desenvolvimento permanece no ambiente interno do projeto.

## Download

Acesse a página de [Releases](https://github.com/jefersonflus/namehostai-cli/releases) e baixe o pacote correspondente ao seu sistema operacional.

A versão inicial inclui `namehost-ai-cli-windows-x64.zip` para Windows 64 bits. Após extrair o pacote, o executável é `namehost.exe`.

## Como funciona

1. Execute `namehost` no terminal.
2. No primeiro uso, escolha o login pelo navegador.
3. O navegador abre o portal NameHost para autenticação.
4. Depois da aprovação, o agente recebe um token de sessão e usa o gateway `https://ia.namehost.com.br`.
5. O token não é exibido nem armazenado como chave de API no projeto.

Em servidores ou sessões SSH, use o fluxo de ativação por dispositivo: o agente mostra um endereço e um código, que devem ser aprovados no portal NameHost.

## Requisitos

- Conta ativa no portal NameHost.
- Acesso à internet.
- Windows 10/11 64 bits para o pacote Windows.
- PowerShell ou Prompt de Comando para uso local.

## Gateway e modelos

O agente usa o mesmo token Bearer nas rotas compatíveis do gateway:

- `GET https://ia.namehost.com.br/v1/models`
- `POST https://ia.namehost.com.br/v1/messages`
- `POST https://ia.namehost.com.br/v1/chat/completions`
- `POST https://ia.namehost.com.br/v1/responses`

O catálogo de modelos e as permissões são determinados pela conta e pela chave NameHost escolhida durante a aprovação no portal.

## Configuração

A configuração do usuário fica no diretório de dados do NameHost. O agente também aceita as variáveis `NAMEHOST_*` documentadas na versão instalada.

Nunca publique tokens, cookies ou arquivos de sessão em issues, commits ou logs.

## Verificação do download

Cada Release informa o SHA-256 do arquivo. No Windows, valide com:

```powershell
Get-FileHash .\namehost-ai-cli-windows-x64.zip -Algorithm SHA256
```

## Atualizações

As versões são publicadas como GitHub Releases. Baixe a nova versão, substitua o executável e mantenha a configuração do usuário. O agente não depende de instalação por loja de aplicativos.

## Suporte

Abra uma issue informando a versão, o sistema operacional e a mensagem de erro. Remova tokens e dados pessoais antes de enviar logs.

## Licença

Consulte os termos publicados junto à Release correspondente.
