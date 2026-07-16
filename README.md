# Xpto Digital ID — Versão estática (Azure Static Web Apps)

Esta é uma versão 100% estática (HTML + CSS + JavaScript no navegador) do protótipo
"Carteira de Identidade Digital", compatível com o Azure Static Web Apps — que **não**
executa um processo ASP.NET Core (Razor Pages/Session) como o projeto original em .NET,
apenas arquivos estáticos (opcionalmente + Azure Functions).

O login e o aceite dos Termos de Uso são simulados com `localStorage` (guardado no
navegador do usuário), o suficiente para demonstrar o fluxo completo do app.

## Fluxo
`index.html` (splash) → `termos.html` (aceite obrigatório) → `login.html` → `carteira.html`

Login de demonstração: matrícula `12345` / senha `1234` (ou `54321` / `4321`).

## Como subir para o GitHub

Dentro desta pasta (`StaticSite`):

```bash
git init
git add .
git commit -m "Versão estática do app Xpto Digital ID"
git branch -M main
git remote add origin https://github.com/thunanchiu/unyleiaidentidade.git
git push -u origin main
```

Se o repositório já tiver algo (ex: README inicial do GitHub), use antes:

```bash
git pull origin main --allow-unrelated-histories
```

## Como criar o Static Web App no Azure

1. Portal do Azure → **Criar um recurso** → **Static Web App**
2. Assinatura / Grupo de recursos: os mesmos que você já usa (ex: `Estudo`)
3. **Nome**: um nome livre, ex: `xpto-digital-id`
4. **Plano de hospedagem**: **Gratuito**
5. **Fonte de implantação**: **GitHub**
   - Clique em **Entrar com o GitHub** e autorize
   - **Organização**: `thunanchiu`
   - **Repositório**: `unyleiaidentidade`
   - **Branch**: `main`
6. **Predefinições de build**: escolha **Custom** (ou "HTML" se aparecer)
   - **Local do aplicativo**: `/` (raiz, pois os arquivos HTML estão direto na raiz do repositório)
   - **Local da API**: deixe em branco (não há API)
   - **Local de saída**: deixe em branco
7. Clique em **Revisar + criar** → **Criar**

O Azure vai commitar automaticamente um arquivo `.github/workflows/azure-static-web-apps-....yml`
no seu repositório. A partir daí, todo `git push` na branch `main` já publica a nova versão
automaticamente (CI/CD).

## Endereço final
Após a criação, o Azure gera uma URL pública do tipo:

```
https://<nome-gerado>.azurestaticapps.net
```

Esse é o link que você pode usar no Passo 6 do estudo de caso (publicação em PWA/loja).
