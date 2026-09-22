# Registro de Atendimentos — Suporte Técnico (Supabase + Vercel)

App web (um único `index.html`) para técnicos registrarem a baixa de
chamados de internet resolvidos por telefone ou WhatsApp, com print de
comprovação. Roda 100% fora do Claude: banco de dados e armazenamento
de arquivos pelo Supabase, hospedagem estática pelo Vercel.

## Stack

- **Frontend**: HTML/CSS/JS puro, um arquivo só (`index.html`)
- **Banco de dados**: Supabase (Postgres) — tabelas `atendimentos`,
  `tecnicos`, `cidades`, `codigos_resolucao`
- **Armazenamento dos prints**: Supabase Storage (bucket `comprovantes`)
- **Hospedagem**: Vercel (deploy automático a cada push)

## Editar as listas (técnicos, cidades, códigos)

As listas dos dropdowns vêm das tabelas `tecnicos`, `cidades` e
`codigos_resolucao` no Supabase (Table Editor). Adicionar, editar ou
desativar (`ativo = false`) um item ali atualiza o app automaticamente
— não precisa mexer no código nem fazer novo deploy.

## Acesso restrito do supervisor

A consulta da tabela e a exportação em CSV ficam bloqueadas por senha
(hash SHA-256 no código, sem senha em texto puro). Existe também um
botão de exclusão total dos registros, protegido por uma segunda senha
diferente da de supervisor.

## Segurança do banco (importante)

Atualmente o Row Level Security (RLS) das tabelas e do bucket de
Storage está **desativado**, para simplificar os testes iniciais —
qualquer pessoa com a chave pública do projeto consegue ler e escrever
nos dados. Antes de usar com dados reais de clientes em produção, vale
configurar políticas de RLS mais restritas.

## Como atualizar

1. Baixe a versão mais recente do `index.html` (gerada pelo Claude).
2. Substitua o arquivo nesta pasta.
3. `git add .`
4. `git commit -m "descrição da mudança"`
5. `git push`

O Vercel redeploya sozinho a cada push.
