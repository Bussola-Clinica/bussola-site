# CHECKLIST — Reconectar Vercel ao bussola-site

**Responsável:** Raphael
**Sintoma:** o site publicado não reflete o conteúdo da `main`. O último deploy
registrado é de 04/08; a `main` está em `b56d5f0` (21/08), com a seção de planos e
o link do LinkedIn do Sidnei já mergeados.

**Diagnóstico:** o código está no lugar certo. `origin/main` aponta para `b56d5f0`
e não há nenhum commit depois dele — ou seja, não é caso de trabalho não commitado
nem de branch errada. O que falta é o deploy. A causa provável é a transferência
do repositório para a org `Bussola-Clinica`: a integração da Vercel é instalada por
org, e uma transferência não leva a instalação junto. O projeto continua existindo
na Vercel, apontando para um caminho de repositório que não recebe mais webhook.

```
[ ] Acessar vercel.com → workspace FoundLab → projeto bussola-site
[ ] Settings → Git → verificar Connected Git Repository
[ ] Se mostrar repo antigo ou desconectado: Disconnect → Connect Git Repository
[ ] Buscar Bussola-Clinica/bussola-site no seletor
[ ] Se a org não aparecer: acessar github.com/apps/vercel/installations/select_target
    e conceder acesso à org Bussola-Clinica e ao repo bussola-site
[ ] Após reconectar: fazer redeploy manual do commit b56d5f0
[ ] Confirmar que bussolaclinica.com reflete a seção de planos e o LinkedIn do Sidnei
```

## Critério de conclusão

Os dois últimos itens são o que fecha o checklist. Reconectar o repositório na tela
de Settings não republica nada sozinho — a Vercel só constrói no próximo evento de
Git. Por isso o redeploy manual de `b56d5f0` é obrigatório, e a confirmação é olhar
o site publicado, não o painel.

## Verificação depois

Vale um commit de teste na `main` para confirmar que o webhook voltou de verdade.
Reconectar e ver o deploy manual funcionar prova que o projeto constrói; só um push
prova que ele constrói **sozinho** — que é o comportamento que se perdeu.
